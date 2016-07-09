title: Configuration
subtitle: Core Module
-------

- [Admin prefix](#admin-prefix)
- [Themes path](#themes-path)
- [Admin theme](#admin-theme)
- [AdminLTE skin](#adminlte-skin)
- [Custom Ckeditor config path]($custom-ckeditor-config)
- [Middleware](#middleware)

This **Core Module** has one main configuration item, you'll find it at `config/asgard.core.core.php`.

## <a class="anchor" name="admin-prefix" href="#admin-prefix">Admin Prefix</a>

With this configuration you can set how you access the admin dashboard. By default it is set to `backend`. Meaning you can access your admin dashboard on the following url `localhost:8000/backend` (if you're using the `artisan serve` command).

``` .language-php
'admin-prefix' => 'backend'
```

## <a class="anchor" name="themes-path" href="#themes-path">Themes Path</a>

This is the location of the Themes.

``` .language-php
'themes_path' => base_path() . '/Themes',
```

## <a class="anchor" name="admin-theme" href="#admin-theme">Admin theme</a>

With this setting you can change the theme used in the administration. Make sure your admin theme has the **type** set to `backend`.

It defaults to `AdminLTE`.


``` .language-php
'admin-theme' => 'AdminLTE',
```


## <a class="anchor" name="adminlte-skin" href="#adminlte-skin">AdminLTE skin</a>

You can customize the AdminLTE colors with this setting. The following colors are available for you to use: 

- skin-blue, 
- skin-green, 
- skin-black, 
- skin-purple, 
- skin-red,
- skin-yellow.

This defaults to the blue skin.

``` .language-php
'skin' => 'skin-blue',
```


## <a class="anchor" name="custom-ckeditor-config" href="#custom-ckeditor-config">Custom Ckeditor Config path</a>

In case you wish to customise ckeditor and the default configuration provided doesn't suit you, you can define a custom ckeditor configuration file here. The paths needs to be relative to the `public/` directory.

Example:

``` .language-php
'ckeditor-config-file-path' => '/assets/config_custom.js',
```


## <a class="anchor" name="middleware" href="#middleware">Middleware</a>

Here you can add or remove middleware of different types of routes (admin, frontend and api). Add your own middleware here on their respective types.