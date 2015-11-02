title: Linking media to object
subtitle: Media Module
-------

- [One to one relation](#one-to-one)
- [One to many relation](#one-to-many)

You can use the media uploaded in any module you make. 

Lets say you have an articles module, and want your article to have a cover image. This is when you'll want a '**one-to-one**' relation type. If for instance you have a product, which can have multiple images, you'll want a '**one-to-many**' relation type.

It is important to note that both types use the same `morphToMany` relation behind the scenes. It's only the UI which changes.

Also important, the partials pre-made for those 2 types, can only be used on the edit page of an object since it needs the id of the current object to make the relation.


### <a name="one-to-one-relation" class="anchor" href="#one-to-one-relation"></a> One to one relation


Like the introduction said, this type of relation is for when you only need one file/image for a particular entity. In addition to this, the image can have a **zone** given. To stay consistent, using the Article module, example from the introduction, that cover image will have a zone of `coverimage`.

That way we can easily get the cover image for a particular article.

#### MediaRelation trait

First thing you need is add the `Modules\Media\Support\Traits\MediaRelation` trait onto your desired *entity* (an eloquent model).

This will add a `files` morphToMany relation onto your entity.

From here you could already start implementing your own field to select a file from the media module, or you can include the partial.

#### Include the partial

Next you can include the `media::admin.fields.file-link` partial, on the edit view only. This needs 3 variables:

- **entityClass**: the class of the linked object. In our example of articles it would be the Articly entity.
- **entityId**: the id of the linked object. In our example this would be the article id.
- **zone**: the name of the zone the image. In our example this would be the coverimage.


``` .language-markup

@include('media::admin.fields.file-link', [
    'entityClass' => 'Modules\\\\Article\\\\Entities\\\\Article',
    'entityId' => $article->id,
    'zone' => 'coverimage'
])
```

This partial is mostly used to display and link images.

#### Getting the thumbnail from controller

The final step is to get the thumbnail from the controller so it can be displayed on the object if there is already a file linked to that object. If you're using the partial from the second step, this would be to display the linked image.

You can inject the `FileRepository` into your constructor or method and use the `findFileByZoneForEntity` method to get your image. This methods has two parameters, the zone name (*string*) and the entity (*object*) it needs to search on.

``` .language-php
$coverimage = $this->file->findFileByZoneForEntity('coverimage', $article);
```

One important note here is **the variable name has to be the same as the zone name**.


### <a name="one-to-many-relation" class="anchor" href="#one-to-many-relation"></a> One to many relation

This resembles very much the one-to-one relation, except the partial to include and the method to call to get all linked files.

#### MediaRelation trait

First thing you need is add the `Modules\Media\Support\Traits\MediaRelation` trait onto your desired *entity* (eg: an eloquent model).

#### Include the partial

Next you can include the `media::admin.fields.file-link-multiple` partial, on the edit view only. This needs 3 variables:

- **entityClass**: the class of the linked object. In our example of articles it would be the Articly entity.
- **entityId**: the id of the linked object. In our example this would be the article id.
- **zone**: the name of the zone the image. In our example this would be the coverimage.


``` .language-markup

@include('media::admin.fields.file-link-multiple', [
    'entityClass' => 'Modules\\\\Product\\\\Domain\\\\Entities\\\\Product',
    'entityId' => $product->id,
    'zone' => 'gallery'
])

```

This partial is mostly used to display and link images.

#### Getting the thumbnails from controller

Now you can use the helper method on the `FileRepository` to fetch all files for the given object. It has also 2 parameters, the zone (*string*) and the entity (*object*) it needs to search on.

``` .language-php
$galleryFiles = $this->file->findMultipleFilesByZoneForEntity('gallery', $product);
```

Again, it is important **the variable name is the same as the zone name**.