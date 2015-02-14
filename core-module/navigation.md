title: Navigation
subtitle: Core Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Single Menu Item](#single-menu-item)
- [Menu With Submenus](#menu-with-submenus)

### <a class="anchor" name="introduction" href="#introduction"></a> Introduction

If you want your module to have its navigation item in the dashboard, it's very easy. AsgardCMS uses the [Laravel-Sidebar](https://github.com/Maatwebsite/Laravel-Sidebar) package. This package enables us to add sidebar items, subitems, groups, append badges, quicklinks etc.

The basic gist is that the core module listens for incoming menu items and loops over them to display the navigation. This works by leveraging Laravel's View Composers.

### <a class="anchor" name="usage" href="#usage"></a> Usage

First thing you have to do is define a view compsoser, in a `composers.php` file for instance.

Attach that view composer the the `partials.sidebar-nav` partial, and as a second argument point to your compose class.

### <a class="anchor" name="single-menu-item" href="#single-menu-item"></a> Single menu item

This is how the page module handles it:

``` .language-php
View::composer('partials.sidebar-nav', 'Modules\Page\Composers\SidebarViewComposer');
```
The corresponding `SidebarViewComposer` looks like this:


``` .language-php
<?php namespace Modules\Page\Composers;

use Illuminate\Contracts\View\View;
use Maatwebsite\Sidebar\SidebarGroup;
use Maatwebsite\Sidebar\SidebarItem;
use Modules\Core\Composers\BaseSidebarViewComposer;
use Modules\Page\Repositories\PageRepository;

class SidebarViewComposer extends BaseSidebarViewComposer
{
    public function compose(View $view)
    {
        $view->sidebar->group('Pages', function (SidebarGroup $group) {
            $group->enabled = false;
            $group->weight = 5;

            $group->addItem('Pages', function (SidebarItem $item) {
                $item->append('admin.page.page.create');
                $item->badge(function ($append, PageRepository $page) {
                    $append->value = $page->countAll();
                });
                $item->route('admin.page.page.index');
                $item->icon = 'fa fa-file';
                $item->name = 'Pages';
                $item->authorize(
                    $this->auth->hasAccess('page.pages.index')
                );
            });
        });
    }
}

```

The important part here is the `$view->sidebar` variable. It is an instance of the `SidebarManager`.

The `apend()` method enables us to append a 'plus' sign right of the menu item which is a link to the given route.

The `badge()` method gives us the option to append a badge, like the example here the closure can be used to inject a class.

The `route()` method sets the URL of the menu item.

The `icon()` like you would imagine gives us the option to prepend an icon.

The `name()` method sets the display text.

A `weight()` method can optionally be used to set the position of the item. The higher the weight, the lower the item will be in the sidebar.

And finally `authorize()` recieves a boolean and determines wether or not to display the item.


### <a class="anchor" name="menu-with-submenus" href="#menu-with-submenus"></a> Menu with submenus

If you wamt a submenu, we basically just add a items to the items collection.

You'll recognise the same keys as previously.

For the User module it looks like the following:

``` .language-php
<?php namespace Modules\User\Composers;

use Illuminate\Contracts\View\View;
use Modules\Core\Composers\BaseSidebarViewComposer;

class SidebarViewComposer extends BaseSidebarViewComposer
{
    public function compose(View $view)
    {
        $view->sidebar->group('Users', function ($group) {
            $group->weight = 1;
            $group->authorize(
                $this->auth->hasAccess('user.users.index') or $this->auth->hasAccess('user.roles.index')
            );

            $group->addItem('Users', function ($item) {

                $item->addItem('users', function ($item) {
                    $item->weight = 0;
                    $item->route('admin.user.user.index');
                    $item->icon = 'fa fa-user';
                    $item->name = 'Users';
                    $item->authorize(
                        $this->auth->hasAccess('user.users.index')
                    );
                });

                $item->addItem('roles', function ($item) {
                    $item->weight = 1;
                    $item->route('admin.user.role.index');
                    $item->icon = 'fa fa-flag-o';
                    $item->name = 'Roles';
                    $item->authorize(
                        $this->auth->hasAccess('user.roles.index')
                    );
                });
            });

        });
    }
}
```

And that is all you have to do to add your menu item.
