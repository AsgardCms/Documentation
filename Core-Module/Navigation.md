# Core module : Navigation

## Introduction

If you want your module to have its navigation item in the dashboard, it's very easy. You can start by reading a [blog post](http://nwidart.com/blog/view-composers-and-view-creators-in-laravel) I wrote about exactly this.

The basic gist is that the core module listens for incomming menu items and loops over them to display the navigation. This works by leveraging Laravel's View Composers.

## Usage

First thing you have to do is define a view compsoser, in a `composers.php` file for instance.

Attach that view composer the the `core::partials.sidebar-nav` partial, as a second argument point to your compose class.

## Single menu item

This is how the dashboard module handles it:

``` php
View::composer('core::partials.sidebar-nav', 'Modules\Dashboard\Composers\SidebarViewComposer');
```
The corresponding `SidebarViewComposer` looks like this:


``` php
<?php namespace Modules\Dashboard\Composers;

class SidebarViewComposer
{
    public function compose($view)
    {
        $view->items->put('dashboard', [
            'weight' => 0,
            'request' => "*/$view->prefix",
            'route' => 'dashboard.index',
            'icon-class' => 'fa fa-dashboard',
            'title' => 'Dashboard',
        ]);
    }
}
```

The important part here is the `$view->items` variable. It is a Laravel Collection. If your menu doesn't have a submenu you can simple put a new item in the collection.

That item has to following keys

```
'weight' => 0 // The position in the menu
'request' => "*/$view->prefix", // When the active class should be applied
'route' => 'dashboard.index', // The route that matches the item
'icon-class' => 'fa fa-dashboard', // The icon class name
'title' => 'Dashboard', // The actual text for the item
```

## Menu with submenus

If you wamt a submenu, we basically just add a child collection, where its first item will be used for the submenu title, and the other are the submenu items.

You'll recognise the same keys as previously.

For the User module it looks like the following:

``` php
<?php namespace Modules\User\Composers;

use Illuminate\Support\Collection;
use Illuminate\Support\Facades\Request;

class SidebarViewComposer
{
    public function compose($view)
    {
        $view->items->put('user', Collection::make([
            [
                'weight' => '1',
                'request' => Request::is("*/{$view->prefix}/users*") or Request::is("*/{$view->prefix}/roles*"),
                'route' => '#',
                'icon-class' => 'fa fa-user',
                'title' => 'Users & Roles',
            ],
            [
                'request' => "*/{$view->prefix}/users*",
                'route' => 'dashboard.user.index',
                'icon-class' => 'fa fa-user',
                'title' => 'Users',
            ],
            [
                'request' => "*/{$view->prefix}/roles*",
                'route' => 'dashboard.role.index',
                'icon-class' => 'fa fa-flag-o',
                'title' => 'Roles',
            ]
        ]));
    }
}
```

And that is all you have to do to add your menu item.


***

[Back to ToC](../readme.md)