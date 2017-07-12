title: File Hooks
subtitle: Media Module
-------

The media module comes with the following hooks. You can hook into those using the usual listener logic.

- [FileIsCreating](#file-is-creating)
- [FileIsUpdating](#file-is-updating)

[Please view the hook section in the Core module.](/docs/v2/core-module/hooks)


## <a class="anchor" name="file-is-creating" href="#file-is-creating">FileIsCreating</a>


## <a class="anchor" name="file-is-updating" href="#file-is-updating">FileIsUpdating</a>

The `FileIsUpdating` has one more method:

- `getFile()`: Will return the file being updated


### <a class="anchor" name="file-is-creating-example" href="#file-is-creating-example">FileIsCreating Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class.

Lets force a lowercase filename:

```.language-php
Event::listen(FileIsCreating::class, function (FileIsCreating $event) {
    $event->setAttributes(['filename' => strtolower($event->getAttribute('filename'))]);
});
```
