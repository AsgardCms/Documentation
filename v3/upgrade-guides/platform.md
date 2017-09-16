title: Upgrade Guide
subtitle: Platform
-------

- [From v2 to v3](#upgrade-3.0)


## <a name="upgrade-3" class="anchor" href="#upgrade-3">From v2 to **v3**</a>

**Upgrade to laravel 5.5**

Follow the [Laravel upgrade guide](https://laravel.com/docs/5.5/upgrade#upgrade-5.5.0) to upgrade your application and modules.

**Re-publish configuration files**

Using the following command you will be able to publish a module config files.

``` .language-bash
php artisan module:publish-config --force
```

If you edited the module configurations, you will need to manually copy over the new files, depending on what you changed, you can also publish each module individually.

**Page translations**

The page translation structure has been changed. Most keys are now at root level. <br/>
This should not impact you unless you published the translation files for page module.

