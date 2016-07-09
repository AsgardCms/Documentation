title: Install or Update a module/theme
subtitle: Core Module
-------

- [Install an existing module/theme](#install-module-theme)
- [Update a module/theme](#update-module-theme)


It's important to know that a module and a theme, is just a simple **composer package**. Meaning that if your module has a dependency on another package or AsgardCMS-module, you can add those in the `require` key of the `composer.json` file of your module.

This also means that modules fetched via composer, **cannot** be edited, those changes will get overwritten in the next `composer update`.

**But how does AsgardCms know to put the modules in the `Modules` folder and themes in the `Themes` folder ?**

It's pretty easy actually, just check the `type` key in your composer.json file.

- For modules: `"type": "asgard-module",`,
- For themes: `"type": "asgard-theme",`.

That's it, thanks to this, AsgardCms knows where to put those packages. Make sure your modules and themes have the correct type set.



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