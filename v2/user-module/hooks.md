title: Hooks
subtitle: User Module
-------

- [Hooking into hooks](#hooking-into-hooks)
- [Example](#example)

The user module comes with the following hooks. You can hook into those using the usual listener logic.

- UserIsCreating
- UserIsUpdating

## <a class="anchor" name="hooking-into-hooks" href="#hooking-into-hooks">Hooking into hooks</a>

To hook into those hooks you can create a listener class that is set to listen on the event you require. All events ending with `IsCreating` and `IsUpdating` across module implementing the [`EntityIsChanging`](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Contracts/EntityIsChanging.php) interface.

In those events you have access to the following methods:

- `getAttributes()`: Will return the current attributes of the entity
- `getAttribute('name', 'default')`: Will return the `name` attribute
- `setAttributes([])`: Will set your given attributes
- `getOriginal()`: Will return the original attributes, untouched by other listeners. Optional parameter can be used to get a specific original key

The `UserIsUpdating` has one more method:

- `getUser()`: Will return the user being updated


## <a class="anchor" name="hook-example" href="#hook-example">Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class. Lets say you want to make sure the first and last names are using an upper case first letter, we could do this:

```.language-php
Event::listen(UserIsCreating::class, function (UserIsCreating $event) {
    $attributes['first_name'] = ucfirst($event->getAttribute('first_name'));
    $attributes['last_name'] = ucfirst($event->getAttributes('last_name'));
    $event->setAttributes($attributes);
});
```

And that's it! This will use those modified attributes before storing a user.
