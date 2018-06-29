title: Upgrade Guide
subtitle: User module
-------

- [From v2 to v3](#upgrade-3.0)


## <a name="upgrade-3.0" class="anchor" href="#upgrade-3.0">From v2 to **v3**</a>

**[> Changelog](https://github.com/AsgardCms/Platform/blob/3.0/Modules/User/changelog.yml)**

**Relations closure change**

If you used the dynamic relations configuration option in the user config file, please update `$self` to `$this` keyword. `$this` is now correctly bound inside the closure.

**Auth:: facade now works with AsgardCMS**

Feel free to use any of the laravel Authentication helpers. Like the `Auth::` facade but also the `@auth` or `@guest`.

**Sidebar: User menu item weight**

The user menu item weight has been changed to `10`.
