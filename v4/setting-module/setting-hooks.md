title: Setting Hooks
subtitle: Setting Module
-------

The setting module comes with the following hooks. You can hook into those using the usual listener logic.

- [SettingIsCreating](#setting-is-creating)
- [SettingIsUpdating](#setting-is-updating)

## <a class="anchor" name="setting-is-creating" href="#setting-is-creating">SettingIsCreating</a>

These methods are available:

- `getSettingName()`: will return the setting name
- `getSettingValues()`: will return the setting value(s)
- `setSettingValues($settingValues)`: set the value for the current setting
- `getOriginal()`: get the original setting values

## <a class="anchor" name="setting-is-updating" href="#setting-is-updating">SettingIsUpdating</a>

The `SettingIsUpdating` has one more method:

- `getSetting()`: Will return the setting being updated


### <a class="anchor" name="setting-is-creating-example" href="#setting-is-creating-example">SettingIsCreating Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class.

Lets say we want to uppercase our `core::template` setting:

```.language-php
Event::listen(SettingIsCreating::class, function (SettingIsCreating $event) {
    if ($event->getSettingName() === 'core::template') {
        $event->setSettingValues('my-template');
    }
});
```


