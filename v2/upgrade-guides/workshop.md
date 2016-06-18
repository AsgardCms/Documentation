title: Upgrade Guide
subtitle: Workshop module
-------

- [From 1.11.0 to 1.12.0](#upgrade-1.12.0)

## <a name="upgrade-1.12.0" class="anchor" href="#upgrade-1.12.0"></a> From 1.11.0 to **1.12.0**

**Translations have been removed**

All translations files were removed from the individual modules and moved to the [Translation](https://github.com/AsgardCms/Translation) module. Therefore you will need to require the Translation module in your project. This can be done by running the following command in your project:

``` .language-bash
composer require asgardcms/translation-module
```
