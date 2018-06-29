title: Adding tags on entities
subtitle: Tag Module
-------

- [Add interface & trait on desired entity](#add-interface-trait)
- [Defining a new namespace to use for tags](#define-namespace)
- [Display the tag field on your views](#display-tags)
- [Store tags](#store-tags)
- [Removing morph relationship on delete of entity](#remove-morph-relationship)


## <a name="add-interface-trait" class="anchor" href="#add-interface-trait">1. Add interface & trait on desired entity</a>

Your entity needs to implement the `Modules\Tag\Contracts\TaggableInterface` interface.

In order for your entity to satisfy this interface it needs to use the following traits:

- `Modules\Core\Traits\NamespacedEntity`
- `Modules\Tag\Traits\TaggableTrait`

Tags are organised by namespace. This is used in order to get the tags for a specific namespace on the display of the field. It also creates tags for that namespace if tags need to be created.
 
By default the `TaggableTrait` will use the full namespace of your entity. However, you can specify a nicer / shorter namespace to use by using the static `$entityNamespace` property on your entity.
 
Example:
 
``` .language-php
protected static $entityNamespace = 'asgardcms/media';
```


## <a name="define-namespace" class="anchor" href="#define-namespace">2. Defining a new namespace to use for tags</a>

In your module Service Provider, `boot()` method, you now need to add the namespace it's going to use. This can be done using the `TagManager` interface.

``` .language-php
$this->app[TagManager::class]->registerNamespace(new File());
```

And with this, the Tag Module is aware of the new namespace.


## <a name="display-tags" class="anchor" href="#display-tags">3. Display the tag field on your views</a>


By using a custom blade directive you can include the tags field on your views. 

- The first argument is the namespace to get the tags for.
- (optional) Second argument is the entity to fetch the tags for (pre-filling the input if tags are present for given entity).
- (optional) Third argument can be a view to use. This will override the default tags view with its input field.
- (optional) Fourth and last argument can be a name to use. This will override the default name for the input field.

```` .language-php
@tags('asgardcms/media', $file)
````


## <a name="store-tags" class="anchor" href="#store-tags">4. Store tags</a>


In your repositories you need to call the `setTags()` method to persist the tags on your entity.

``` .language-php
$file->setTags(array_get($data, 'tags'));
```

And that's all on how to use tags for your entities.


## <a name="remove-morph-relationship" class="anchor" href="#remove-morph-relationship">(optional) Removing morph relationship on delete of entity</a>

When you delete the entity to which there are tags linked to, you might want to delete the relation between your entity and the tags (the morph relationship). This relationship can be viewed in the `tag__tagged` table.

To delete this link when deleting your entity, you can call the following method in your repository, for instance the destroy method:

```.language-php
public function destroy($page)
{
    $page->untag();

    event(new PageWasDeleted($page));

    return $page->delete();
}
```

When the `untag()` methods gets no argument, it will remove all links for the entity.
