title: Tag Hooks
subtitle: Tag Module
-------

The tag module comes with the following hooks. You can hook into those using the usual listener logic.

- [TagIsCreating](#tag-is-creating)
- [TagIsUpdating](#tag-is-updating)

[Please view the hook section in the Core module.](/docs/v2/core-module/hooks)


## <a class="anchor" name="tag-is-creating" href="#tag-is-creating">TagIsCreating</a>


## <a class="anchor" name="tag-is-updating" href="#tag-is-updating">TagIsUpdating</a>

The `UserIsUpdating` has one more method:

- `getTag()`: Will return the tag being updated


### <a class="anchor" name="tag-is-creating-example" href="#tag-is-creating-example">TagIsCreating Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class.

Lets say we

```.language-php
Event::listen(UserIsCreating::class, function (UserIsCreating $event) {
    $attributes['first_name'] = ucfirst($event->getAttribute('first_name'));
    $attributes['last_name'] = ucfirst($event->getAttribute('last_name'));
    $event->setAttributes($attributes);
});
```
