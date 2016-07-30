title: Upgrade Guide
subtitle: Setting module
-------

- [From v1 to v2](#upgrade-2.0)
- [From 1.12.1 to 1.13.0](#upgrade-1.13.0)



## <a name="upgrade-2.0" class="anchor" href="#upgrade-2.0">From v1 to **v2**</a>

**[> Changelog](https://github.com/AsgardCms/Setting/blob/2.0/changelog.yml)**

No breaking changes.


## <a name="upgrade-1.13.0" class="anchor" href="#upgrade-1.13.0">From 1.12.1 to **1.13.0**</a>

**Translations have been removed**

All translations files were removed from the individual modules and moved to the [Translation](https://github.com/AsgardCms/Translation) module. Therefore you will need to require the Translation module in your project. This can be done by running the following command in your project:

``` .language-bash
composer require asgardcms/translation-module
```

