title: Menu Hooks
subtitle: Menu Module
-------

The menu module comes with the following hooks. You can hook into those using the usual listener logic.

- [MenuIsCreating](#menu-is-creating)
- [MenuIsUpdating](#menu-is-updating)
- [MenuItemIsCreating](#menu-item-is-creating)
- [MenuItemIsUpdating](#menu-item-is-updating)

[Please view the hook section in the Core module.](/docs/v2/core-module/hooks)


## <a class="anchor" name="menu-is-creating" href="#menu-is-creating">MenuIsCreating</a>


## <a class="anchor" name="menu-is-updating" href="#menu-is-updating">MenuIsUpdating</a>

The `MenuIsUpdating` has one more method:

- `getMenu()`: Will return the menu being updated


### <a class="anchor" name="menu-is-creating-example" href="#user-is-creating-example">MenuIsCreating Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class.

Lets say you want to make the menu name lowercase:

```.language-php
Event::listen(MenuIsCreating::class, function (MenuIsCreating $event) {
    $event->setAttributes(['name' => strtolower($event->getAttribute('name'))]);
});
```


## <a class="anchor" name="menu-item-is-creating" href="#menu-item-is-creating">MenuItemIsCreating</a>


## <a class="anchor" name="menu-item-is-updating" href="#menu-item-is-updating">MenuItemIsUpdating</a>

The `MenuItemIsUpdating` has one more method:

- `getMenuItem()`: Will return the menu item being updated

