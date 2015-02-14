title: Themes
subtitle: Themes
-------

- [Folder structure](#folder-structure)
- [Commands](#commands)
- [Linking to theme assets](#linking-to-theme-assets)
- [Display a theme page](#display-a-theme-page)
- [Elixer publish helper](#elixir)

In this section we will go over on how to create and manage themes.

### <a name="folder-structure" class="anchor" href="#folder-structure"></a> Folder structure

A theme has to have a `theme.json` file which will contain the theme name, its description and type (frontend | backend). All your views will be located in the `views` directory. Those views will use assets that are located in the `assets` folder. This asset folder will be publised in the public directory. I'd recommend placing your `less`, `sass`, `coffeescript` files inside a `resources` folder which thanks to gulp will be published to the `assets` folder. 

You can create a theme by creating a folder inside the `Themes` folder.

This would be a typical type structure:

```
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

``` json
{
  "name": "AdminLTE",
  "description": "This is an administration theme",
  "type": "backend"
}
```


### <a name="commands" class="anchor" href="#commands"></a> Commands

As you can see the assets live in the `Themes` folder in the root directory. To publish the assets to the public directory and make the accessible to the webserver, you have to use a publish command:

``` .language-bash
php artisan asgard:publish:theme
```


### <a name="linking-to-theme-assets" class="anchor" href="#linking-to-theme-assets"></a> Linking to theme assets

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

### <a name="display-a-theme-page" class="anchor" href="#display-a-theme-page"></a> Display a theme page

To display a page from a theme, or using its layout, there is nothing new; use the `View::make` as normal.

For instance if you have set the active theme to `Demo`, when you use `View::make('index')`, it'll check for the page inside your Demo theme folder `Themes/demo/index.blade.php`.


### <a name="display-a-theme-page" class="anchor" href="#elixir"></a> Elixer publish helper

Since all assets need to be published to the `public/` folder you can use the following custom **mix** for [Laravel Elixir](http://laravel.com/docs/5.0/elixir).

Place this at the top of your `Gulpfile`:


``` .language-javascript
var gulp = require("gulp");
var shell = require('gulp-shell');
var elixir = require('laravel-elixir');

elixir.extend("stylistPublish", function() {
    gulp.task("stylistPublish", function() {
        gulp.src("").pipe(shell("php ../../artisan stylist:publish"));
    });

    this.registerWatcher("stylistPublish", "**/*.less");

    return this.queueTask("stylistPublish");
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