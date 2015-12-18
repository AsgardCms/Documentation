title: Upgrade Guide
subtitle: Platform
-------

- [From 1.12.0 to 1.13.0](#upgrade-1.13.0)

## <a name="upgrade-1.13.0" class="anchor" href="#upgrade-1.13.0"></a> From 1.12.0 to **1.13.0**

### New Job class

The laravel abstract `Job` class has been added in `app/Jobs/Job.php`. Add the [`Job`](https://github.com/AsgardCms/Platform/blob/master/app/Jobs/Job.php) class to your project in that same location (`app/Jobs/Job.php`).
