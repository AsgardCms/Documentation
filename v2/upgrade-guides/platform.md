title: Upgrade Guide
subtitle: Platform
-------

- [From v2.4.0 to v2.5.0](#upgrade-2.5.0)
- [From v2.3.0 to v2.4.0](#upgrade-2.4.0)
- [From v1 to v2](#upgrade-2.0)
- [From 1.12.0 to 1.13.0](#upgrade-1.13.0)


## <a name="upgrade-2.5" class="anchor" href="#upgrade-2.5">From v2.4.0 to **v2.5.0**</a>

**New cache driver**

A new cache driver was added specifically for translations. [You can view this configuration here](https://github.com/AsgardCms/Platform/blob/2.0/config/cache.php#L74-L77). You can also set the environment variable `TRANSLATIONS_CACHE_DRIVER` in your `.env` file to use redis for example or any other driver.


## <a name="upgrade-2.4" class="anchor" href="#upgrade-2.4">From v2.3.0 to **v2.4.0**</a>

**Local Filesystem**

The local filesystem drivers was updated to match laravel. [You will need to apply those changes.](https://github.com/AsgardCms/Platform/blob/2.0/config/filesystems.php#L59-L60)

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
