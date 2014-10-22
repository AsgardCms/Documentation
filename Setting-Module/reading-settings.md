# Setting module : Reading settings


## Injecting the repository


To use a setting you can inject the setting repository interface into your method/constructor.

``` php
/**
 * @var SettingRepository
 */
private $setting;

public function __construct(SettingRepository $setting)
{
  $this->setting = $setting;
}
```

## Using the repository

Once this is done you can use the repository to get a setting specific to a module, or if you don't want/know the module only the setting name.

### Without specifying the module

``` php
$this->setting->findSettingForModule('site-name');
```

### With specifying the module


``` php
$this->setting->findSettingForModule('posts-per-page', 'blog');
```

