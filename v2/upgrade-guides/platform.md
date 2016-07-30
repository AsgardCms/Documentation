title: Upgrade Guide
subtitle: Platform
-------


- [From v1 to v2](#upgrade-2.0)
- [From 1.12.0 to 1.13.0](#upgrade-1.13.0)



## <a name="upgrade-2.0" class="anchor" href="#upgrade-2.0">From v1 to **v2**</a>

**Upgrade to laravel 5.2**

Follow the [Laravel upgrade guide](https://laravel.com/docs/5.2/upgrade#upgrade-5.2.0) to upgrade your application and modules.

**Re-problish configuration files**

Configuration files across modules has been changed, mostly the `permissions.php` files.

Using the following command you will be able to publish a module config files.

``` .language-bash
php artisan module:publish-config --force
```

If you edited the module configurations, you will need to manually copy over the new files, depending on what you changed, you can also publish each module individually.



## <a name="upgrade-1.13.0" class="anchor" href="#upgrade-1.13.0">From 1.12.0 to **1.13.0**</a>

**New Job class**

The laravel abstract `Job` class has been added in `app/Jobs/Job.php`. Add the `Job` class ([view class](https://github.com/AsgardCms/Platform/blob/master/app/Jobs/Job.php)) to your project in that same location (`app/Jobs/Job.php`).
