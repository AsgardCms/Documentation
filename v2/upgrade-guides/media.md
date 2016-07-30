title: Upgrade Guide
subtitle: Media module
-------

- [From v1 to v2](#upgrade-2.0)
- [From 1.22.0 to 1.23.0](#upgrade-1.23.0)
- [From 1.21.0 to 1.22.0](#upgrade-1.22.0)
- [From 1.17.0 to 1.18.0](#upgrade-1.18.0)
- [From 1.16.0 to 1.17.0](#upgrade-1.17.0)
- [From 1.15.0 to 1.16.0](#upgrade-1.16.0)

## <a name="upgrade-2.0" class="anchor" href="#upgrade-2.0">From v1 to **v2**</a>

**[> Changelog](https://github.com/AsgardCms/Media/blob/2.0/changelog.yml)**

**New blade directives**

It isn't needed anymore to use the `@include` directives. Instead the menu module comes with its own directives, `@mediaSingle` and `@mediaMultiple`.

Learn all about those new directives on the [updated documentation](https://asgardcms.com/docs/v2/media-module/linking-media-to-entities).

These directes can now also be used on the *create views*!


## <a name="upgrade-1.23.0" class="anchor" href="#upgrade-1.23.0">From 1.22.0 to **1.23.0**</a>

**events.php configuration file not needed**

This file is not needed anymore.


## <a name="upgrade-1.22.0" class="anchor" href="#upgrade-1.22.0">From 1.21.0 to **1.22.0**</a>

**New configuration file `config/asgard.media.events.php`**

This new configuration file is needed for allowing to include linking media partials on the create views of your forms. It contains will contain arrow of events that the media module will hook into. 

Create the file your self in the configuration folder with the [following contents](https://github.com/AsgardCms/Media/blob/master/Config/events.php).



## <a name="upgrade-1.18.0" class="anchor" href="#upgrade-1.18.0">From 1.17.0 to **1.18.0**</a>

**Queued jobs**

The `RefreshThumbnailCommand` now uses a queued job as well as a previously queue closure in the `FileService` class was abstracted to a queued job. 

This requires the presence of the abstract [`Job`](https://github.com/AsgardCms/Platform/blob/master/app/Jobs/Job.php) class in `app/Jobs/Job.php`.


## <a name="upgrade-1.17.0" class="anchor" href="#upgrade-1.17.0">From 1.16.0 to **1.17.0**</a>

**Translations have been removed**

All translations files were removed from the individual modules and moved to the [Translation](https://github.com/AsgardCms/Translation) module. Therefore you will need to require the Translation module in your project. This can be done by running the following command in your project:

``` .language-bash
composer require asgardcms/translation-module
```

## <a name="upgrade-1.16.0" class="anchor" href="#upgrade-1.16.0">From 1.15.0 to **1.16.0**</a>

**New `filesystem` configuration item**

A new `filesystem` configuration item was added to the media module config file. By default it is set to the local file system.

After updating the media module, you can either set that new configuration key in the `Config/asgard.media.config.php` file as follows:


``` .language-php
'filesystem' => 'local',
```

Or if you're running version `1.19` or higher of the media module, by running the following command:

``` .language-bash
php artisan vendor:publish --provider="Modules\Media\Providers\MediaServiceProvider" --force --tag="config"
```
