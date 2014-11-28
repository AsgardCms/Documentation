# Themes

In this section we will go over on how to create and manage themes.


## Folder structure

The structure for a theme is completely up to you. Only requirement is to have an `assets` folder containing you assets (css, js, sass, less, etc.).

You can create a theme by creating a folder inside the `Themes` folder. The name of the folder has to be **all lowercase**.



## Commands

As you can see the assets live in the `Themes` folder in the root directory. To publish the assets to the public directory and make the accessible to the webserver, you have to use a publish command:

```
php artisan asgard:publish:theme
```


## Linking to theme assets

To link to a theme asset you can use the following helpers:

``` html
<link rel="stylesheet" type="text/css" href="{{ theme_url() }}/css/styles.css">
<script src="{{ theme_url() }}/js/main.min.js"></script>
```

