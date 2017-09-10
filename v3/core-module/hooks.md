title: Hooks
subtitle: Core Module
-------

AsgardCMS gives you the ability to hook into different part of the application. This lets you change data before it's used somewhere else, or any other feature that can take advantage of hookable events.

- [Hooking into entity hooks](#hooking-into-entity-hooks)
- [EditorIsRendering](#editor-is-rendering)
- [CollectingAssets](#collecting-assets)

## <a class="anchor" name="hooking-into-entity-hooks" href="#hooking-into-entity-hooks">Hooking into entity hooks</a>

To hook into those hooks you can create a listener class that is set to listen on the event you require. All events ending with `IsCreating` and `IsUpdating` across module implementing the [`EntityIsChanging`](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Contracts/EntityIsChanging.php) interface.

In those events you have access to the following methods:

- `getAttributes()`: Will return the current attributes of the entity
- `getAttribute('name', 'default')`: Will return the `name` attribute
- `setAttributes([])`: Will set your given attributes
- `getOriginal()`: Will return the original attributes, untouched by other listeners. Optional parameter can be used to get a specific original key

The `IsUpdating` hooks will usually also have a method to get the entity being updated.

## <a class="anchor" name="editor-is-rendering" href="#editor-is-rendering">EditorIsRending</a>

This hook enables you to change which editor is used in the backend. Two editors are provided by default: **ckeditor** and **simplemde**. Ckeditor is activated by default.

The event uses the asset pipeline, which requires your assets to be defined on the asset manager before hand. How to do this is explained [here](/docs/v2/core-module/assetmanager).

### Adding textarea fields with swappable wysiwygs in your modules

Since a textarea needs to custom code to allow for the wysiwyg to be swappable, we've made a convenient helper blade directive for easy of use. It's now a simple matter of calling the following:

#### Translatable

``` .language-php
// Create
@editor('body', trans('page::pages.form.body'), old("{$lang}.body"), $lang)

// Edit
<?php $old = $page->hasTranslation($lang) ? $page->translate($lang)->body : '' ?>
@editor('body', trans('page::pages.form.body'), old("$lang.body", $old), $lang)
```

#### Normal

Same editor directive, with the locale omitted.

``` .language-php
// Create
@editor('body', trans('page::pages.form.body'), old('body'))

// Edit
@editor('body', trans('page::pages.form.body'), old('body', $old))
```

### Creating a custom editor

This [event](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Events/EditorIsRendering.php) has the following methods:

- `addJs($asset)`: add a javascript asset.
- `addCss($asset)`: add a css asset.
- `setEditorClass($editorClass)`: set which class to use on the `textarea` element
- `setEditorJsPartial($editorJsPartial)`: in case your favorite editor requires some javascript initialisation, you can provide a partial to do that there. Remember to use the `@push('js-stack')` in that partial.
- `setEditorCssPartial($editorCssPartial)`: in case you favorite editor requires custom css, you can provide a partial to do that here. Remember to use the `push('css-stack')` in that partial.
- `getEditorClass()`: returns the editor class
- `getEditorJsPartial()`: get the js partial name
- `getEditorCssPartial()`: get the css partial name

These methods will suffice to most needs of custom wywisyg editors. However, if your editor requires more than just the textarea field, you can overwrite the laravel component completely and use your own. It is probably a good idea to copy the [existing components](https://github.com/AsgardCms/Platform/tree/2.0/Modules/Core/Resources/views/components) to have something to start with.

When you've created your own components, you can set them by using this API on the `EditorIsRendering` event:

- `getI18nComponentName()`: Get the component name for the translatable textarea
- `setI18nComponentName($componentName)`: Set the component name for the translatable textarea
- `getComponentName()`: Get the component name for the textarea
- `setComponentName($componentName)`: Set the component name for the textarea

#### Using your new editor

You can change which event listener is used by changing the `asgard.core.core.wysiwyg-handler` configuration option.

AsgardCMS comes with the following options built-in:

- `\Modules\Core\Events\Handlers\LoadCkEditor::class`
- `\Modules\Core\Events\Handlers\LoadSimpleMde::class`

#### How to render markdown

If you do choose the markdown editor, you might wonder how to parse and render the markdown, thankfully there's a hook for that: [`ContentIsRendering`](/docs/v2/page-module/page-hooks#content-is-rendering). AsgardCMS also comes with a ready to use event listener to render markdown using league/commonmark: [`RenderMarkdown`](https://github.com/AsgardCms/Platform/blob/2.0/Modules/Core/Events/Handlers/RenderMarkdown.php). Simply use this listener on the ContentIsRendering event and you're good to go.

## <a class="anchor" name="collecting-assets" href="#collecting-assets">CollectingAssets</a>

With this hook you can add your assets on every route, or optionally on some routes. The following methods are available:

- `requireCss($asset)` Require a css asset.
- `requireJs($asset)`: Require a js asset.
- `onRoute($route)`: Check if the given route matches the current route. Supports wildcards with `*`.
- `onRoutes($routes)`: Check if the given array of routes matches the current route. Supports wildcards with `*`.

### CollectingAssets Example

For the Page Module, we need iCheck on the create and edit pages, and Datatables on the page index.

```.language-php
Event::listen(CollectingAssets::class, function (CollectingAssets $event) {
    if ($event->onRoutes(['*page*create', '*page*edit'])) {
        $event->requireCss('icheck.blue.css');
        $event->requireJs('icheck.js');
    }
    if ($event->onRoute('*page*index')) {
        $event->requireCss('dataTables.bootstrap.css');
        $event->requireJs('jquery.dataTables.js');
        $event->requireJs('dataTables.bootstrap.js');
    }
});
```


