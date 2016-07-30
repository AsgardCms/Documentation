title: Sidebar Management
subtitle: Core Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Single Menu Item](#single-menu-item)
- [Menu With Submenus](#menu-with-submenus)
- [Overwriting Default Sidebars](#overwrite-default-sidebars)

## <a class="anchor" name="introduction" href="#introduction">Introduction</a>

If you want your module to have its navigation item in the dashboard, it's very easy. AsgardCMS uses the [Laravel-Sidebar](https://github.com/Maatwebsite/Laravel-Sidebar) package. This package enables us to add sidebar items, subitems, groups, append badges, quicklinks etc.

The basic gist is that the core module listens for incoming menu items and loops over them to display the navigation. This works by leveraging Laravel's View Composers.

## <a class="anchor" name="usage" href="#usage">Usage</a>

First thing you have to do is creating a sidebar extender. Under the `Sidebar` namespace in your module.

> Note: this is automatically generated when using the Module Scaffold command.

## <a class="anchor" name="single-menu-item" href="#single-menu-item">Single menu item</a>

This is how the page module handles it, in `Modules/Pages/Sidebar/SidebarExtender.php`:

``` .language-php
<?php namespace Modules\Page\Sidebar;

use Maatwebsite\Sidebar\Badge;
use Maatwebsite\Sidebar\Group;
use Maatwebsite\Sidebar\Item;
use Maatwebsite\Sidebar\Menu;
use Modules\Core\Contracts\Authentication;
use Modules\Page\Repositories\PageRepository;

class SidebarExtender implements \Maatwebsite\Sidebar\SidebarExtender
{
    /**
     * @var Authentication
     */
    protected $auth;

    /**
     * @param Authentication $auth
     *
     * @internal param Guard $guard
     */
    public function __construct(Authentication $auth)
    {
        $this->auth = $auth;
    }

    /**
     * @param Menu $menu
     *
     * @return Menu
     */
    public function extendWith(Menu $menu)
    {
        $menu->group(trans('core::sidebar.content'), function (Group $group) {
            $group->item(trans('page::pages.title.pages'), function (Item $item) {
                $item->icon('fa fa-file');
                $item->weight(1);
                $item->route('admin.page.page.index');
                $item->badge(function (Badge $badge, PageRepository $page) {
                    $badge->setClass('bg-green');
                    $badge->setValue($page->countAll());
                });
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
<?php namespace Modules\User\Sidebar;

use Maatwebsite\Sidebar\Group;
use Maatwebsite\Sidebar\Item;
use Maatwebsite\Sidebar\Menu;
use Modules\Core\Contracts\Authentication;

class SidebarExtender implements \Maatwebsite\Sidebar\SidebarExtender
{
    /**
     * @var Authentication
     */
    protected $auth;

    /**
     * @param Authentication $auth
     *
     * @internal param Guard $guard
     */
    public function __construct(Authentication $auth)
    {
        $this->auth = $auth;
    }

    /**
     * @param Menu $menu
     *
     * @return Menu
     */
    public function extendWith(Menu $menu)
    {
        $menu->group(trans('workshop::workshop.title'), function (Group $group) {

            $group->item(trans('user::users.title.users'), function (Item $item) {
                $item->weight(0);
                $item->icon('fa fa-user');
                $item->authorize(
                    $this->auth->hasAccess('user.users.index') or $this->auth->hasAccess('user.roles.index')
                );

                $item->item(trans('user::users.title.users'), function (Item $item) {
                    $item->weight(0);
                    $item->icon('fa fa-user');
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

        return $menu;
    }
}
```
You can find this class in `Modules/User/Sidebar/SidebarExtender.php`

And that is all you have to do to add your menu item.


## <a class="anchor" name="overwrite-default-sidebars" href="#overwrite-default-sidebars">Overwriting Default Sidebars</a>

AsgardCMS comes with default modules, which all have their own sidebar class. If the structure those classes don't correspond to what you would like to have, you have the possibility to overwrite those sidebar classes, on a per module basis.

Let say you want to overwrite the sidebar of the Menu module. 

Open the published menu module config file located at `config/asgard/menu/config.php`.

In here you will find a `custom-sidebar` key. This is where you can define your own sidebar class. Enter the full namespace to your customised sidebar class here and that will be used instead of the one provided by the menu module.

This works for any AsgardCMS module. If the config key `custom-sidebar` does not exist, it can be added and will be used.