title: Hooks
subtitle: Core Module
-------

AsgardCMS gives you the ability to hook into different part of the application. This lets you change data before it's used somewhere else, or any other feature that can take advantage of hookable events.

- [Hooking into entity hooks](#hooking-into-entity-hooks)
- [EditorIsRendering](#editor-is-rendering)

## <a class="anchor" name="hooking-into-entity-hooks" href="#hooking-into-entity-hooks">Hooking into entity hooks</a>

To hook into those hooks you can create a listener class that is set to listen on the event you require. All events ending with `IsCreating` and `IsUpdating` across module implementing the [`EntityIsChanging`](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Contracts/EntityIsChanging.php) interface.

In those events you have access to the following methods:

- `getAttributes()`: Will return the current attributes of the entity
- `getAttribute('name', 'default')`: Will return the `name` attribute
- `setAttributes([])`: Will set your given attributes
- `getOriginal()`: Will return the original attributes, untouched by other listeners. Optional parameter can be used to get a specific original key

The `IsUpdating` hooks will usually also have a method to get the entity being updated.

## <a class="anchor" name="editor-is-rendering" href="#editor-is-rendering">EditorIsRending</a>

This hook enabled you to change which editor is used in the backend. Two editors are provider by default ckeditor and simplemde. Ckeditor is activated by default.

The event uses the asset pipeline, which requires your assets to be defined on the asset manager before hand. How to do this is explained [here](/docs/v2/core-module/assetmanager).

This [event](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Events/EditorIsRendering.php) has the following methods:

- `addJs($asset)`: add a javascript asset.
- `addCss($asset)`: add a css asset.
- `setEditorClass($editorClass)`: set which class to use on the `textarea` element
- `setEditorJsPartial($editorJsPartial)`: in case your favorite editor requires some javascript initialisation, you can provide a partial to do that there. Remember to use the `@push('js-stack')` in that partial.
- `setEditorCssPartial($editorCssPartial)`: in case you favorite editor requires custom css, you can provide a partial to do that here. Remember to use the `push('css-stack')` in that partial.
- `getEditorClass()`: returns the editor class
- `getEditorJsPartial()`: get the js partial name
- `getEditorCssPartial()`: get the css partial name


You can change which event listener is used by changing the `asgard.core.core.wysiwyg-handler` configuration option.

AsgardCMS comes with the following options built-in:

- `\Modules\Core\Events\Handlers\LoadCkEditor::class`
- `\Modules\Core\Events\Handlers\LoadSimpleMde::class`
