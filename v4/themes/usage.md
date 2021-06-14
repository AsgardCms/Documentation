title: Using and developing themes
subtitle: Themes
-------

- [Folder structure](#folder-structure)
- [Commands](#commands)
- [Linking to theme assets](#linking-to-theme-assets)
- [Display a theme page](#display-a-theme-page)
- [Elixer publish helper](#elixir)
- [Ovewriting core theme views)[#core_modules_overwrite]

In this section we will go over on how to create and manage themes. You can view a demo frontend, [Flatly](https://github.com/AsgardCms/Flatly-theme) theme and [demo backend theme](https://github.com/AsgardCms/AdminLTE) for your inspiration.

## <a name="folder-structure" class="anchor" href="#folder-structure">Folder structure</a>

A theme has to have a `theme.json` file which will contain the theme name, its description and type (frontend | backend). All your views will be located in the `views` directory. Those views will use assets that are located in the `assets` folder. This asset folder will be published in the public directory. I'd recommend placing your `less`, `sass`, `coffeescript` files inside a `resources` folder which thanks to gulp will be published to the `assets` folder. 

You can create a theme by creating a folder inside the `Themes` folder.

This would be a typical type structure:

``` .language-markup
.
Themes/
├── Demo
│   ├── assets
│   |	└── js
│   |	├── css
│   |	├── fonts
│   |	├── img
│   ├── resources
│   |	└── less
│   |	├── coffee
│   ├── views
│   ├── bower.json
│   ├── composer.json
│   ├── gulpfile
│   ├── theme.json
│   ├── package.json
```

A `theme.json` file looks like this: 

``` .language-javascript
{
  "name": "AdminLTE",
  "description": "This is an administration theme",
  "type": "backend"
}
```
The `theme.json` file has to have a `type` key. This has to be either **backend** or **frontend**. 

The primary difference between both, beyond the obvious reason, is that the **backend** theme *won't* show up in the settings module in the theme dropdown.

To set a backend theme, you need to edit the `config/asgard.core.core.php` config file and set the `admin-theme` option. The has to correspond with the `name` key in `module.json`.


## <a name="commands" class="anchor" href="#commands">Commands</a>

As you can see the assets live in the `Themes` folder in the root directory. To publish the assets to the public directory and make the accessible to the webserver, you have to use a publish command:

``` .language-bash
php artisan asgard:publish:theme
```


## <a name="linking-to-theme-assets" class="anchor" href="#linking-to-theme-assets">Linking to theme assets</a>

To link to a theme asset you can use the following helpers:

``` .language-markup
{!! Theme::style('css/vendor/bootstrap.min.css') !!}

{!! Theme::script('js/vendor/jquery.min.js') !!}
```
These will directly output the `<style>` and `<script>` tags.

If you want to directly get a URL of a resource you can use the following helper:

``` .language-markup
<link rel="shortcut icon" href="{{ Theme::url('favicon.ico') }}">
```

## <a name="display-a-theme-page" class="anchor" href="#display-a-theme-page">Display a theme page</a>

To display a page from a theme, or using its layout, there is nothing new; use the `View::make` as normal.

For instance if you have set the active theme to `Demo`, when you use `View::make('index')`, it'll check for the page inside your Demo theme folder `Themes/demo/index.blade.php`.


## <a name="elixir" class="anchor" href="#elixir">Elixir publish helper</a>

Since all assets need to be published to the `public/` folder you can use the following custom **mix** for [Laravel Elixir](http://laravel.com/docs/5.1/elixir).

Place this at the top of your `Gulpfile`:


``` .language-javascript
var gulp = require("gulp");
var shell = require('gulp-shell');
var elixir = require('laravel-elixir');
var themeInfo = require('./theme.json');

var Task = elixir.Task;

elixir.extend('stylistPublish', function() {
    new Task('stylistPublish', function() {
        return gulp.src("").pipe(shell("php ../../artisan stylist:publish " + themeInfo.name));
    });
});
```

With this defined, in your `Gulpfile` you can now do the following:

``` .language-javascript
mix
    .less([
       "main.less"
    ])
   .stylistPublish();
```

Elixir will now compile `main.less`, and publish the compiled css to the `public/` folder.

## <a name="core_modules_overwrite" class="anchor" href="#core_modules_overwrite">Overwrite code modules views</a>

The system allows to overwrite any of the modules that are core to the system inside the theme itself. To allow this you must enable some configuration settings.

Inside the config/asgard/core/core.php: set _enable-theme-overrides_ to *true*

Then check if the core module allows to overwrite the views.
To see this, check inside the module for the _useViewNamespaces_ variable inside it's _Config/config.php_ file. If found you can overwrite the views for the frontend & backend themes.

The, add the view into the theme inside the _modules/<module_name>/_ folder.

An example to clarify this: To overwrite the Modules/User/Resources/view/public/login.blade.php you modify the configuration as indicated before and then, copy the file into Themes/MyTheme/views/modules/user/public/login.blade.php and make you modifications.
