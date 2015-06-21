title: Adding settings
subtitle: Setting Module
-------

- [Registering translatable settings](#registering-translatable-settings)
- [Registering plain settings](#registering-plain-settings)

Adding settings for you module is very easy. All you need to do is add a `settings.php` configuration file in `YourModule/config/settings.php`, and return an array of settings you want.

### <a name="registering-translatable-settings" class="anchor" href="#registering-translatable-settings"></a> Registering translatable settings

The settings are registered in the following manner:


``` .language-php

return [
    'posts-per-page' => [
        'description' => trans('blog::settings.posts-per-page'),
        'view' => 'text',
        'translatable' => true,
        'default' => 15,
    ],
    'this-is-a-checkbox' => [
        'description' => 'This is a checkbox',
        'view' => 'checkbox',
        'translatable' => true,
    ],
    'this-is-a-textarea' => [
        'description' => 'This is a textarea',
        'view' => 'textarea',
        'translatable' => true,
    ],
];

```

The **array key** being the setting name, holding an array of information. 

The information array needs the following:

- a `description` key: this will be the label / placeholder, 
- a `view` key: which points to the view holding the field,
- a `translatable` key: defines if the setting is translatable (set in multiple languages)
- a `default` key (*optional*): defines a default value for your setting if none is present and none is set in the third argument of `Setting::get()`.


### <a name="registering-plain-settings" class="anchor" href="#registering-plain-settings"></a> Registering Plain settings

Not every setting has to be translatable, plain settings are settings that aren't translated.

``` .language-php
 'plain-non-translated-setting' => [
    'description' => 'A plain setting',
    'view' => 'text',
    'default' => 'your default value',
],
```
