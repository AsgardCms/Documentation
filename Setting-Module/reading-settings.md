# Setting module : Reading settings


## Injecting the interface


To use a setting you can inject the [setting interface](https://github.com/nWidart-Modules/Core/blob/master/Contracts/Setting.php) into your method/constructor.

``` php
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

## Using the interface

Once this is done you can use the interface to get a setting, in a given locale.
Since settings can be translatable or not, you can optionnaly specify the language.

### Get setting in current locale

``` php
$siteName = $this->setting->get('core::site-name', App::getLocale())
```

### Get a non translatable setting


``` php
$postsPerPage = $this->setting->get('blog::posts-per-page');
```

