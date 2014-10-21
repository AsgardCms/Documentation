# Setting module : Adding settings

Adding settings for you module is very easy. All you need to do is add a `settings.php` configuration file in `YourModule/config/settings.php`, and return an array of settings you want.

## Registering settings

The settings are registered in the following manner:


``` php

return [
    'posts-per-page' => [
        'description' => trans('blog::settings.posts-per-page'),
        'view' => 'setting::admin.partials.module-text-field'
    ],
    'this-is-a-checkbox' => [
        'description' => 'This is a checkbox',
        'view' => 'setting::admin.partials.module-checkbox-field'
    ],
    'this-is-a-textarea' => [
        'description' => 'This is a textarea',
        'view' => 'setting::admin.partials.module-textarea-field'
    ],
];

```

The **array key** beeing the setting name, holding an array of information. 

The information array needs a `description` key, this will be the label / placeholder. And a `view` key which point to the view holding the field. 



  

