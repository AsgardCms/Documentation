title: Helpers
subtitle: Core Module
-------

- [on_route](#on_route)

### <a class="anchor" name="on_route" href="#on_route"></a> Introduction

The `on_route()` helper function is pretty straightforward, it allows you to quickly check if the user is on the given route. This is usually used for setting active classes on a menu.

Example usage: 

``` .language-php
<li class="{{ on_route('user.account') ? 'active' : '' }}">
    <a href="{{ route('user.account') }}">Account</a>
</li>
```

