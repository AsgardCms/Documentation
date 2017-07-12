title: User Hooks
subtitle: User Module
-------

The user module comes with the following hooks. You can hook into those using the usual listener logic.

- [UserIsCreating](#user-is-creating)
- [UserIsUpdating](#user-is-updating)

[Please view the hook section in the Core module.](/docs/v2/core-module/hooks)


## <a class="anchor" name="user-is-creating" href="#user-is-creating">UserIsCreating</a>


## <a class="anchor" name="user-is-updating" href="#user-is-updating">UserIsUpdating</a>

The `UserIsUpdating` has one more method:

- `getUser()`: Will return the user being updated


### <a class="anchor" name="user-is-creating-example" href="#user-is-creating-example">UserIsCreating Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class. Lets say you want to make sure the first and last names are using an upper case first letter, we could do this:

```.language-php
Event::listen(UserIsCreating::class, function (UserIsCreating $event) {
    $attributes['first_name'] = ucfirst($event->getAttribute('first_name'));
    $attributes['last_name'] = ucfirst($event->getAttribute('last_name'));
    $event->setAttributes($attributes);
});
```
