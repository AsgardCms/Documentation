title: Custom Fields
subtitle: Page Module
-------

- [Configuration](#configuration)
- [Hooking in events](#events)
- [Usage](#usage)

It is often required to add more fields to a page than the default provided ones. For this reason you can add any type of custom field to the Page Module. 

For an in-depth overview you can watch the following video on [adding custom fields to the page module](https://www.youtube.com/watch?v=HpzYIWOdzv8).


## <a name="configuration" class="anchor" href="#configuration"></a> Configuration


### Defining the fields

In the Page module config file located at `Config/asgard.page.config.php` you'll see the following configuration options:

``` .language-php
'partials' => [
    'translatable' => [
        'create' => [],
        'edit' => [],
    ],
    'normal' => [
        'create' => [],
        'edit' => [],
    ],
],
```

In these arrays you can give on array of fields for translatable fields (create & edit) and non translatable fields (create & edit). Those will be shown on the page create and edit views.


### Defining the relation

In that same config file you'll also see a `relations` key, just as with the User module, you can add dynamic relations with the Page entity. This will mostly be with your custom module that will have the entity with the additional data to be stored

## <a name="events" class="anchor" href="#events"></a> Events

The way to 'intercept' the posted data, is by hooking into the `PageWasCreated` and `PageWasUpdated` events. These events both have the `pageId` (int) and `data` (array). The `data` contains the **posted data**.


## <a name="usage" class="anchor" href="#usage"></a> Usage

With the configuration setup, and your event handlers in place, you'll have the custom data stored in database. To display the data you can simply call the relation you setup in the configuration as a *method*.

``` .language-php
$page->yourRelation()->custom_field
```
