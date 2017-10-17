title: Upgrade Guide
subtitle: Platform
-------

- [From v3.1.0 to v3.2.0](#upgrade-3.2)
- [From v3.0.0 to v3.1.0](#upgrade-3.1)
- [From v2 to v3](#upgrade-3.0)


## <a name="upgrade-3.2" class="anchor" href="#upgrade-3.2">From v3.1.1 to **v3.2.0**</a>

**New way to register translations for VueJs**

In order to let VueJS know about your translations you need to use the `LoadingBackendTranslations` hook to register your translations. This can be done like so in your module Service Provider:

```.language-php
$this->app['events']->listen(LoadingBackendTranslations::class, function (LoadingBackendTranslations $event) {
    $event->load('pages', array_dot(trans('page::pages')));
});
```


**Recompile assets**

Due to changes in core assets, you will have to recompile assets. You can do this with the following commands:

- `npm insall`
- `npm run dev`


## <a name="upgrade-3.1" class="anchor" href="#upgrade-3.1">From v3.0.3 to **v3.1.0**</a>

**Recompile assets**

Due to changes in core assets, you will have to recompile assets. You can do this with the following commands:

- `npm insall`
- `npm run dev`


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

