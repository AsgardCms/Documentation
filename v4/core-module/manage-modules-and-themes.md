title: Manage Modules and Themes
subtitle: Core Module
-------

- [Install an existing module/theme](#install-module-theme)
- [Update a module/theme](#update-module-theme)
- [Download an existing Module](#download-module)
- [Delete an existing Module](#delete-module)


It's important to know that a module and a theme, is just a simple **composer package**. Meaning that if your module has a dependency on another package or AsgardCMS-module, you can add those in the `require` key of the `composer.json` file of your module.

This also means that modules fetched via composer, **cannot** be edited, those changes will get overwritten in the next `composer update`.

**But how does AsgardCms know to put the modules in the `Modules` folder and themes in the `Themes` folder ?**

It's pretty easy actually, just check the `type` key in your composer.json file.

- For modules: `"type": "asgard-module",`,
- For themes: `"type": "asgard-theme",`.

That's it, thanks to this, AsgardCms knows where to put those packages. Make sure your modules and themes have the correct type set.

In case you don't want to use composer to download a package in your project, scroll down to the [Download an existing Module](#download-module) section.



## <a class="anchor" name="install-module-theme" href="#install-module-theme">Install an existing module/theme</a>

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


## <a class="anchor" name="update-module-theme" href="#update-module-theme">Update a module/theme</a>

To fetch updates from a module or a theme you can run `composer update`.

## <a class="anchor" name="download-module" href="#download-module">Download an existing Module</a>

This is an alternative way of downloading existing modules. This won't use composer, instead it will directly download and place the desired modules in the `Modules/` directory. There are some advantages and disadvantages to doing it this way versus using composer.

**Advantages to using composer:**

1. Easy updates

**Disadvantages to using composer:**

1. Not easy to customise the module if needed, since any changes made, will be overwritten on your next `composer update`


**Advantages to using download feature:**

1. Customisable out of the box

**Disadvantages to using download feature:**

1. No version management with the original repository

After having downloaded a module, you can instantly start to customise it to your needs, and add it to your version control system.

### Downloading a module

The download command is simple:

``` .language-bash
php artisan asgard:download:module vendor/name
```


Let's say you want to download the [AsgardCMS/Contact](https://github.com/AsgardCms/Contact) module. Run this command to do so:


``` .language-bash
php artisan asgard:download:module asgardcms/contact
```

This will download the Contact module in your `Modules/` folder.

**Running migrations**

``` .language-bash
php artisan asgard:download:module asgardcms/contact --migrations
```

**Running seeds**

``` .language-bash
php artisan asgard:download:module asgardcms/contact --seeds
```

**Publishing module assets**

``` .language-bash
php artisan asgard:download:module asgardcms/contact --assets
```


Of course all those options, can be specified together:

``` .language-bash
php artisan asgard:download:module asgardcms/contact --migrations --seeds --assets
# or
php artisan asgard:download:module asgardcms/contact --demo
```

### Download a specific branch

The previous commands requires the wanted module to have a **github release**. This might not always be the case (though recommended). For this situation you can specify which branch to download using the `--branch` option

``` .language-bash
php artisan asgard:download:module asgardcms/contact --branch=master
```

This will not download the latest release, but instead the master branch.


## <a class="anchor" name="delete-module" href="#delete-module">Delete an existing Module</a>

If you want to remove a module, you can use the following command:

``` .language-bash
php artisan asgard:delete:module ModuleName --migrations
```

This will remove the module's tables, and remove any user or role that had permissions for this module.

