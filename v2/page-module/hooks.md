title: Hooks
subtitle: Page Module
-------

- [Hooking into hooks](#hooking-into-hooks)
- [Example](#example)

The page module comes with the following hooks. You can hook into those using the usual listener logic.

- [PageIsCreating](#page-is-creating)
- [PageIsUpdating](#page-is-updating)
- [ContentIsRendering](#content-is-rendering)

[Please view the hook section in the Core module.]()

## <a class="anchor" name="page-is-creating" href="#page-is-creating">PageIsCreating</a>


## <a class="anchor" name="page-is-updating" href="#page-is-updating">PageIsUpdating</a>

The `PageIsUpdating` has one more method:

- `getPage()`: Will return the page being updated


### <a class="anchor" name="page-is-updating-example" href="#page-is-updating-example">PageIsUpdating Example</a>

To keep the example simple we're going to use an inline listener using a closure instead of a full class.

Lets say you want to upper case the page titles:

```.language-php
Event::listen(PageIsUpdating::class, function (PageIsUpdating $event) {
    $attributes = [
        'en' => ['title' => strtoupper($this->getAttributes('en.title'))]
        'fr' => ['title' => strtoupper($this->getAttributes('fr.title'))]
    ];
    $event->setAttributes($attributes);
});
```

## <a class="anchor" name="content-is-rendering" href="#content-is-rendering">ContentIsRendering</a>

This hook is used in the body Accessor of a page. Every time you'll call `$page->body` this hook will be triggered. You can still use `->getOriginal('body')` on the PageTranslation entity like any laravel model to bypass this accessor.

Available methods:

- `getBody()`: Will return the current body content
- `setBody('')`: Sets the body element
- `getOriginal()`: Get the original body without any changes by other listeners

You could use this hook to add short codes to your page body section for example.

### <a class="anchor" name="content-is-rendering-example" href="#content-is-rendering-example">ContentIsRendering Example</a>

```.language-php
Event::listen(ContentIsRendering::class, function (ContentIsRendering $event) {
    $content = str_replace('[shortcode]', 'My Awesome Code', $event->getBody(); 
    $event->setBody($content);
});
```
