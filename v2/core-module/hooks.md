title: Hooks
subtitle: Core Module
-------

AsgardCMS gives you the ability to hook into different part of the application. This lets you change data before it's used somewhere else, or any other feature that can take advantage of hookable events.

- [Hooking into entity hooks](#hooking-into-entity-hooks)



## <a class="anchor" name="hooking-into-entity-hooks" href="#hooking-into-entity-hooks">Hooking into entity hooks</a>

To hook into those hooks you can create a listener class that is set to listen on the event you require. All events ending with `IsCreating` and `IsUpdating` across module implementing the [`EntityIsChanging`](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Contracts/EntityIsChanging.php) interface.

In those events you have access to the following methods:

- `getAttributes()`: Will return the current attributes of the entity
- `getAttribute('name', 'default')`: Will return the `name` attribute
- `setAttributes([])`: Will set your given attributes
- `getOriginal()`: Will return the original attributes, untouched by other listeners. Optional parameter can be used to get a specific original key

The `IsUpdating` hooks will usually also have a method to get the entity being updated.
