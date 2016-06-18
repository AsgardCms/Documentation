title: Upgrade Guide
subtitle: User module
-------

- [From 1.13.1 to 1.14.0](#upgrade-1.14.0)
- [From 1.11.0 to 1.12.0](#upgrade-1.12.0)

## <a name="upgrade-1.14.0" class="anchor" href="#upgrade-1.14.0"></a> From 1.13.1 to **1.14.0**

**Translations have been removed**

All translations files were removed from the individual modules and moved to the [Translation](https://github.com/AsgardCms/Translation) module. Therefore you will need to require the Translation module in your project. This can be done by running the following command in your project:

``` .language-bash
composer require asgardcms/translation-module
```

## <a name="upgrade-1.12.0" class="anchor" href="#upgrade-1.12.0"></a> From 1.11.0 to **1.12.0**

**New authentication views**

All authentication views were updated to the latest version of AdminLTE. If you were using the default authentication views and had them published, you will need to re-publish those views. This can be done with the following command:

``` .language-bash
php artisan vendor:publish --provider="Modules\User\Providers\UserServiceProvider" --force
```

