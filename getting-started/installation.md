title: Installation
subtitle: Getting Started
-------

- [Minimum System Requirements](#minimum-system-requirements)
- [Install AsgardCMS](#install-asgardcms)
- [Updating modules and themes](#updating-modules-and-themes)
- [Installing modules and themes](#installing-modules-and-themes)

## <a name="minimum-system-requirements" class="anchor" href="#minimum-system-requirements"></a> Minimum System Requirements

To be able to run AsgardCMS you have to meet the following requirements:

- PHP 5.5.9 or higher
- PDO PHP Extension
- cURL PHP Extension
- OpenSSL PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- Mcrypt PHP Extension
- GD PHP Library
- MySql 5.5
- One of the following cache drivers: `memcached`, `redis`, `apc`. (defaults to `array`)

## <a name="install-asgardcms" class="anchor" href="#install-asgardcms"></a> Install AsgardCMS

If you prefer a video to see how the installation process goes, [watch the install video](https://www.youtube.com/watch?v=MeX_D-aql6g).


### Get AsgardCMS

``` .language-bash
composer create-project asgardcms/platform your-project-name
```

### Create a database

### Install your preferred user system

- Sentinel (installed by default) 

More user implementations may be offered later on.


### Run the install command

Now run `php artisan asgard:install` command to perform to start the installation process.

This install command will perform the following actions:

- Setup database information
- Running migrations
- Running seeds
- Publishing assets
- Create a first admin account


## Enjoy

You can now login on `/auth/login` with your email and password asked during the install command. After you've logged in you'll be able to access the administration panel on the `/backend` URI.

### Feedback, ideas, etc.
If you have **feedback** to give, **ideas** you would like implemented, by all means share them on the [dedicated uservoice page](http://asgardcms.uservoice.com/). Do not hesitate to share! 

For **issues/bugs** your having, you can use the Github Issues to post those. All issues are grouped on the [AsgardCms/Platform](https://github.com/AsgardCms/Platform/issues) repository.

If you just want to **talk**, join [our Slack channel](http://slack.asgardcms.com/).

Thank you for your participation!


## <a name="updating-modules-and-themes" class="anchor" href="#updating-modules-and-themes"></a> Updating modules and themes

It's important to know that a module and a theme, is just a simple composer package. Meaning that if your module has a dependency on another package or AsgardCms-module, you can add those in the `require` key of the `composer.json` file of your module.

This also means that modules fetched via composer, **cannot** be edited, those changes will get overwritten in the next `composer update`.

**But how does AsgardCms know to put the modules in the `Modules` folder and themes in the `Themes` folder ?**

It's pretty easy actually, just check the `type` key in your composer.json file.

- For modules: `"type": "asgard-module",`,
- For themes: `"type": "asgard-theme",`.

That's it, thanks to this, AsgardCms knows where to put those packages. Make sure your modules and themes have the correct type set.

## <a name="installing-modules-and-themes" class="anchor" href="#installing-modules-and-themes"></a> Installing modules and themes

Now that you know that a module or theme is a simple composer package, to install one on you AsgardCms project, just run the usual `composer require vendor/name` in your terminal.

If there are additional steps required to install the module, for instance running migrations, the module will have this stated in its readme.md file.

### Running module migrations

To run the migrations of a module, run the following in your terminal:

``` .language-bash
php artisan module:migrate ModuleName
```

### Running module seeds

Run the following command in your terminal:

```.language-bash
php artisan module:seed ModuleName
```


### Publishing module assets

Module assets are located in the `Assets/` directory of the module. The have those copied in your `public/` folder run the following command:

``` .language-bash
php artisan module:publish ModuleName
```

This will publish the module assets in the following directory:

``` .language-bash
public/modules/ModuleName
```

### Publishing module translation files

Sometimes you'll want to change the copy of static texts of a particular module. If that module is a module fetched with composer, you have to treat that module as a composer package, meaning you cannot perform changes in that module, or those changes will get overwritten in the next `composer update`.

Module translation files can be published by running the following command in your terminal:

``` .language-bash
php artisan module:publish-translation ModuleName
```

This will publish the translation files in the following directory:

``` .language-bash
resources/lang/ModuleName
```
