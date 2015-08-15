title: Reading settings
subtitle: Setting Module
-------

- [Injecting the interface](#injecting-the-interface)
- [Using the interface](#using-the-interface)
	- [Get setting in current locale](#get-setting-in-current-locale)
	- [Get a non translatable setting](get-a-non-translatable-setting)
- [Using the helper function](#using-the-helper-function)
- [Using the facade](#using-the-facade)

## <a name="injecting-the-interface" class="anchor" href="#injecting-the-interface"></a> Injecting the interface

To use a setting you can inject the [setting interface](https://github.com/nWidart-Modules/Core/blob/master/Contracts/Setting.php) into your method/constructor.

``` .language-php
use Modules\Core\Contracts\Setting;

...

/**
 * @var Setting
 */
private $setting;

public function __construct(Setting $setting)
{
    $this->setting = $setting;
}
```

## <a name="using-the-interface" class="anchor" href="#using-the-interface"></a> Using the interface

Once this is done you can use the interface to get a setting, in a given locale.
Since settings can be translatable or not, you can optionally specify the language.

### <a name="get-setting-in-current-locale" class="anchor" href="#get-setting-in-current-locale"></a> Get setting in current locale

``` .language-php
$siteName = $this->setting->get('core::site-name', locale())
```

### <a name="get-a-non-translatable-setting" class="anchor" href="#get-a-non-translatable-setting"></a> Get a non translatable setting

``` .language-php
$postsPerPage = $this->setting->get('blog::posts-per-page');
```

## <a name="using-the-helper-function" class="anchor" href="#using-the-helper-function"></a> Using the helper function

In your views you can directly use the `setting()` function.

To get the site name setting in the core module:

``` .language-php
{{ setting('core::site-name') }}
```


## <a name="using-the-facade" class="anchor" href="#using-the-facade"></a> Using the facade

**Depreciated.**

In views you can use the `Setting` facade with the `get()` method.

To get the site name setting in the core module:

``` .language-php
{{ Setting::get('core::site-name') }}
```
