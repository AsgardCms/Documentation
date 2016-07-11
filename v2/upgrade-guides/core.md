title: Upgrade Guide
subtitle: Core module
-------

- [From v1 to v2](#upgrade-2.0)


## <a name="upgrade-2.0" class="anchor" href="#upgrade-2.0">From v1 to **v2**</a>

**Re-problish configuration files**

Configuration files across modules has been changed, mostly the `permissions.php` files.

Using the following command you will be able to publish a module config files.

``` .language-bash
php artisan vendor:publish --provider="Modules\Core\Providers\CoreServiceProvider" --force
```

If you edited the module configurations, you will need to manually copy over the new files, depending on what you changed, you can also publish each module individually.