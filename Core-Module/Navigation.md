title: Navigation
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Single Menu Item](#single-menu-item)
- [Menu With Submenus](#menu-with-submenus)

### <a class="anchor" name="introduction" href="#introduction"></a> Introduction

If you want your module to have its navigation item in the dashboard, it's very easy. You can start by reading a [blog post](http://nwidart.com/blog/view-composers-and-view-creators-in-laravel) I wrote about exactly this.

The basic gist is that the core module listens for incoming menu items and loops over them to display the navigation. This works by leveraging Laravel's View Composers.

### <a class="anchor" name="usage" href="#usage"></a> Usage

First thing you have to do is define a view compsoser, in a `composers.php` file for instance.

Attach that view composer the the `core::partials.sidebar-nav` partial, as a second argument point to your compose class.

### <a class="anchor" name="single-menu-item" href="#single-menu-item"></a> Single menu item

This is how the dashboard module handles it:

``` .language-php
View::composer('core::partials.sidebar-nav', 'Modules\Dashboard\Composers\SidebarViewComposer');
```
The corresponding `SidebarViewComposer` looks like this:


``` .language-php
<?php namespace Modules\Dashboard\Composers;

use Illuminate\Contracts\View\View;
use Modules\Core\Composers\BaseSidebarViewComposer;

class SidebarViewComposer extends BaseSidebarViewComposer
{
    public function compose(View $view)
    {
        $view->items->put('dashboard', [
            'weight' => 0,
            'request' => "*/$view->prefix",
            'route' => 'dashboard.index',
            'icon-class' => 'fa fa-dashboard',
            'title' => 'Dashboard',
            'permission' => $this->auth->hasAccess('dashboard.index')
        ]);
    }
}
```

The important part here is the `$view->items` variable. It is a Laravel Collection. If your menu doesn't have a submenu you can simple put a new item in the collection.

That item has to following keys

``` .language-php
'weight' => 0 // The position in the menu
'request' => "*/$view->prefix", // When the active class should be applied
'route' => 'dashboard.index', // The route that matches the item
'icon-class' => 'fa fa-dashboard', // The icon class name
'title' => 'Dashboard', // The actual text for the item
'permission' => $this->auth->hasAccess('dashboard.index') // The required permission to be able to see the menu item
```

### <a class="anchor" name="menu-with-submenus" href="#menu-with-submenus"></a> Menu with submenus

If you wamt a submenu, we basically just add a child collection, where its first item will be used for the submenu title, and the other are the submenu items.

You'll recognise the same keys as previously.

For the User module it looks like the following:

``` .language-php
<?php namespace Modules\User\Composers;

use Illuminate\Support\Collection;
use Illuminate\Support\Facades\Request;
use Illuminate\Contracts\View\View;
use Modules\Core\Composers\BaseSidebarViewComposer;

class SidebarViewComposer extends BaseSidebarViewComposer
{
    public function compose(View $view)
    {
        $view->items->put('user', Collection::make([
            [
                'weight' => '1',
                'request' => Request::is("*/{$view->prefix}/users*") or Request::is("*/{$view->prefix}/roles*"),
                'route' => '#',
                'icon-class' => 'fa fa-user',
                'title' => 'Users & Roles',
                'permission' => $this->auth->hasAccess('users.index') or $this->auth->hasAccess('roles.index')
            ],
            [
                'request' => "*/{$view->prefix}/users*",
                'route' => 'dashboard.user.index',
                'icon-class' => 'fa fa-user',
                'title' => 'Users',
                'permission' => $this->auth->hasAccess('users.index')
            ],
            [
                'request' => "*/{$view->prefix}/roles*",
                'route' => 'dashboard.role.index',
                'icon-class' => 'fa fa-flag-o',
                'title' => 'Roles',
                'permission' => $this->auth->hasAccess('roles.index')
            ]
        ]));
    }
}
```

And that is all you have to do to add your menu item.
