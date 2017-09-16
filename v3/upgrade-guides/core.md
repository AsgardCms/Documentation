title: Upgrade Guide
subtitle: Core module
-------

- [From v2 to v3](#upgrade-3.0)


## <a name="upgrade-3.0" class="anchor" href="#upgrade-3.0">From v2 to **v3**</a>

**[> Changelog](https://github.com/AsgardCms/Platform/blob/3.0/Modules/Core/changelog.yml)**

**Authorization middleware**

The `Authorization` middleware now returns a 403 forbidden when a permission is missing, instead of 401.
