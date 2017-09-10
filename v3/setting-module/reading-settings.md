title: Reading settings
subtitle: Setting Module
-------

- [Injecting the interface](#injecting-the-interface)
- [Using the interface](#using-the-interface)
	- [Get setting in current locale](#get-setting-in-current-locale)
	- [Get a non translatable setting](get-a-non-translatable-setting)
- [Using the @setting blade directive](#blade-directive)
- [Using the helper function](#using-the-helper-function)
- [Using the facade](#using-the-facade)

## <a name="injecting-the-interface" class="anchor" href="#injecting-the-interface">Injecting the interface</a>

To use a setting you can inject the [setting interface](https://github.com/AsgardCms/Setting/blob/2.0/Contracts/Setting.php) into your method/constructor.

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

## <a name="using-the-interface" class="anchor" href="#using-the-interface">Using the interface</a>

Once this is done you can use the interface to get a setting, in a given locale.
Since settings can be translatable or not, you can optionally specify the language.

### <a name="get-setting-in-current-locale" class="anchor" href="#get-setting-in-current-locale">Get setting in current locale</a>

``` .language-php
$siteName = $this->setting->get('core::site-name', locale())
```

### <a name="get-a-non-translatable-setting" class="anchor" href="#get-a-non-translatable-setting">Get a non translatable setting</a>

``` .language-php
$postsPerPage = $this->setting->get('blog::posts-per-page');
```

## <a name="blade-directive" class="anchor" href="#blade-directive">Using the @setting blade directive</a>

In your views you can call the `@setting()` blade directive.

``` .language-php
@setting('core::site-name');

// Get the setting value in a specific locale
@setting('core::site-name', 'fr');

// Set a custom default value
@setting('core::site-name', null, 'Default name');
```

## <a name="using-the-helper-function" class="anchor" href="#using-the-helper-function">Using the helper function</a>

In your views or any other class you can directly use the `setting()` function.

To get the site name setting in the core module:

``` .language-php
{{ setting('core::site-name') }}
```


## <a name="using-the-facade" class="anchor" href="#using-the-facade">Using the facade</a>

> Depreciated.

In views you can use the `Setting` facade with the `get()` method.

To get the site name setting in the core module:

``` .language-php
{{ Setting::get('core::site-name') }}
```
