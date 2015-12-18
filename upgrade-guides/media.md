title: Upgrade Guide
subtitle: Media module
-------

- [From 1.17.0 to 1.18.0](#upgrade-1.18.0)
- [From 1.16.0 to 1.17.0](#upgrade-1.17.0)


## <a name="upgrade-1.18.0" class="anchor" href="#upgrade-1.18.0"></a> From 1.17.0 to **1.18.0**

**Queued jobs**

The `RefreshThumbnailCommand` now uses a queued job as well as a previously queue closure in the `FileService` class was abstracted to a queued job. 

This requires the presence of the abstract [`Job`](https://github.com/AsgardCms/Platform/blob/master/app/Jobs/Job.php) class in `app/Jobs/Job.php`.


## <a name="upgrade-1.17.0" class="anchor" href="#upgrade-1.17.0"></a> From 1.16.0 to **1.17.0**

**Translations have been removed**

All translations files were removed from the individual modules and moved to the [Translation](https://github.com/AsgardCms/Translation) module. Therefore you will need to require the Translation module in your project. This can be done by running the following command in your project:

``` .language-bash
composer require asgardcms/translation-module
```
