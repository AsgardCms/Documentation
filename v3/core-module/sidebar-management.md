title: Sidebar Management
subtitle: Core Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Register a sidebar](#register-sidebar)
- [Single Menu Item](#single-menu-item)
- [Menu With Submenus](#menu-with-submenus)
- [Overwriting Default Sidebars](#overwrite-default-sidebars)

## <a class="anchor" name="introduction" href="#introduction">Introduction</a>

If you want your module to have its navigation item in the dashboard, it's very easy. AsgardCMS uses the [Laravel-Sidebar](https://github.com/Maatwebsite/Laravel-Sidebar) package. This package enables us to add sidebar items, subitems, groups, append badges, quicklinks etc.

The basic gist is that the core module listens for incoming menu items and loops over them to display the navigation. This works by leveraging Laravel's View Composers.

## <a class="anchor" name="usage" href="#usage">Usage</a>

First thing you have to do is creating a sidebar extender. Under the `Events/Handlers` namespace in your module.

> Note: this is automatically generated when using the Module Scaffold command.

## <a class="anchor" name="usage" href="#register-sidebar">Register a sidebar</a>

**Note that is is automatically done for you when scaffolding a module**

You can register your sidebars using the `BuildingSidebar` hook. 

In your module service provider use the `CanGetSidebarClassForModule` helper trait. With this trait you'll be able to use a helper method `getSidebarClassForModule`.

Next, in the register method of your module service provider hook into the `BuildingSidebar` hook like so:

```.language-php
$this->app['events']->listen(
    BuildingSidebar::class,
    $this->getSidebarClassForModule('page', RegisterPageSidebar::class)
);
```


## <a class="anchor" name="single-menu-item" href="#single-menu-item">Single menu item</a>

This is how the page module handles it, in `Modules/Pages/Events/Handlers/RegisterPageSidebar.php`:

``` .language-php
<?php

namespace Modules\Page\Events\Handlers;

use Maatwebsite\Sidebar\Group;
use Maatwebsite\Sidebar\Item;
use Maatwebsite\Sidebar\Menu;
use Modules\Core\Sidebar\AbstractAdminSidebar;

class RegisterPageSidebar extends AbstractAdminSidebar
{
    /**
     * @param Menu $menu
     * @return Menu
     */
    public function extendWith(Menu $menu)
    {
        $menu->group(trans('core::sidebar.content'), function (Group $group) {
            $group->item(trans('page::pages.pages'), function (Item $item) {
                $item->icon('fa fa-file');
                $item->weight(10);
                $item->route('admin.page.page.index');
                $item->authorize(
                    $this->auth->hasAccess('page.pages.index')
                );
            });
        });

        return $menu;
    }
}

```


The `append()` method enables us to append a 'plus' sign right of the menu item which is a link to the given route.

The `badge()` method gives us the option to append a badge, like the example here the closure can be used to inject a class.

The `route()` method sets the URL of the menu item.

The `icon()` like you would imagine gives us the option to prepend an icon.

The `name()` method sets the display text.

A `weight()` method can optionally be used to set the position of the item. The higher the weight, the lower the item will be in the sidebar.

And finally `authorize()` receives a boolean and determines whether or not to display the item.


## <a class="anchor" name="menu-with-submenus" href="#menu-with-submenus">Menu with submenus</a>

If you want a submenu, we basically just add a items to the items collection.

You'll recognise the same methods as mentioned on the single item.

For the User module it looks like the following:

``` .language-php
<?php

namespace Modules\User\Events\Handlers;

use Maatwebsite\Sidebar\Group;
use Maatwebsite\Sidebar\Item;
use Maatwebsite\Sidebar\Menu;
use Modules\Core\Sidebar\AbstractAdminSidebar;

class RegisterUserSidebar extends AbstractAdminSidebar
{
    /**
     * Method used to define your sidebar menu groups and items
     * @param Menu $menu
     * @return Menu
     */
    public function extendWith(Menu $menu)
    {
        $menu->group(trans('workshop::workshop.title'), function (Group $group) {
            $group->item(trans('user::users.title.users'), function (Item $item) {
                $item->weight(10);
                $item->icon('fa fa-users');
                $item->authorize(
                    $this->auth->hasAccess('user.users.index') or $this->auth->hasAccess('user.roles.index')
                );

                $item->item(trans('user::users.title.users'), function (Item $item) {
                    $item->weight(0);
                    $item->icon('fa fa-users');
                    $item->route('admin.user.user.index');
                    $item->authorize(
                        $this->auth->hasAccess('user.users.index')
                    );
                });

                $item->item(trans('user::roles.title.roles'), function (Item $item) {
                    $item->weight(1);
                    $item->icon('fa fa-flag-o');
                    $item->route('admin.user.role.index');
                    $item->authorize(
                        $this->auth->hasAccess('user.roles.index')
                    );
                });
            });
        });
        $menu->group(trans('user::users.my account'), function (Group $group) {
            $group->weight(110);
            $group->item(trans('user::users.profile'), function (Item $item) {
                $item->weight(0);
                $item->icon('fa fa-user');
                $item->route('admin.account.profile.edit');
            });
            $group->item(trans('user::users.api-keys'), function (Item $item) {
                $item->weight(1);
                $item->icon('fa fa-key');
                $item->route('admin.account.api.index');
                $item->authorize(
                    $this->auth->hasAccess('account.api-keys.index')
                );
            });
        });

        return $menu;
    }
}
```
You can find this class in `Modules/User/Events/Handlers/RegisterUserSidebar.php`

And that is all you have to do to add your menu item.


## <a class="anchor" name="overwrite-default-sidebars" href="#overwrite-default-sidebars">Overwriting Default Sidebars</a>

AsgardCMS comes with default modules, which all have their own sidebar class. If the structure those classes don't correspond to what you would like to have, you have the possibility to overwrite those sidebar classes, on a per module basis.

Let say you want to overwrite the sidebar of the Menu module. 

Open the published menu module config file located at `config/asgard/menu/config.php`.

In here you will find a `custom-sidebar` key. This is where you can define your own sidebar class. Enter the full namespace to your customised sidebar class here and that will be used instead of the one provided by the menu module.

This works for any AsgardCMS module. If the config key `custom-sidebar` does not exist, it can be added and will be used.