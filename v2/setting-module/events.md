title: Events
subtitle: Setting Module
-------

The following events are triggered in the Setting Module:

- [SettingWasCreated](#setting-was-created)
- [SettingWasUpdate](#setting-was-updated)


## <a name="setting-was-created" class="anchor" href="#setting-was-created">SettingWasCreated</a>

Triggered when a setting that wasn't already present in the settings table has been created. You have access to the setting **name** (*string*), whether it is **translatable** (*bool*) and its **values** (*array|string*).


## <a name="setting-was-updated" class="anchor" href="#setting-was-updated">SettingWasUpdated</a>


Triggered when a setting was updated. You have access to the setting **name**, whether it is **translatable** (*bool*), its **values** (*array|string*) (*string*) and the **old values** (*array|string*).