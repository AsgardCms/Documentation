title: Helpers
subtitle: Core Module
-------

- [on_route](#on_route)
- [locale](#locale)
- [Is module enabled](#is_module_enabled)

## <a class="anchor" name="on_route" href="#on_route">On route</a>

The `on_route()` helper function is pretty straightforward, it allows you to quickly check if the user is on the given route. This is usually used for setting active classes on a menu.

Example usage: 

``` .language-php
<li class="{{ on_route('user.account') ? 'active' : '' }}">
    <a href="{{ route('user.account') }}">Account</a>
</li>
```


## <a class="anchor" name="locale" href="#locale">Locale</a>

The `locale()` helper function is used to **get the current active locale** on the application. 

An optional argument can be given to **set the application locale**.

## <a class="anchor" name="is_module_enabled" href="#is_module_enabled">Is module enabled</a>

The `is_module_enabled($moduleName)` functions returns `true` if the given module name is enabled or `false` if not.