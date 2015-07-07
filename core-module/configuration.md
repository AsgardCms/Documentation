title: Configuration
subtitle: Core Module
-------

- [Admin prefix](#admin-prefix)
- [Admin theme](#admin-theme)
- [AdminLTE skin](#adminlte-skin)

This **Core Module** has one main configuration item, you'll find it at `config/asgard.core.core.php`.

## <a class="anchor" name="admin-prefix" href="#admin-prefix"></a> Admin Prefix

With this configuration you can set how you access the admin dashboard. By default it is set to `backend`. Meaning you can access your admin dashboard on the following url `localhost:8000/backend` (if you're using the `artisan serve` command).

``` language-php
'admin-prefix' => 'backend'
```


## <a class="anchor" name="admin-theme" href="#admin-theme"></a> Admin theme

With this setting you can change the theme used in the administration. Make sure your admin theme has the type set to `backend`.

It defaults to `AdminLTE`.


``` .language-php
'admin-theme' => 'AdminLTE',
```


## <a class="anchor" name="adminlte-skin" href="#adminlte-skin"></a> AdminLTE skin

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

