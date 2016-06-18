title: Linking media to object
subtitle: Media Module
-------

- [One to one relation](#one-to-one-relation)
- [One to many relation](#one-to-many-relation)
- [Deleting the polymorphic relation upon deletion of related model](#delete-polymorphic-relation)

You can use the media uploaded in any module you make. 

Lets say you have an articles module, and want your article to have a cover image. This is when you'll want a '**one-to-one**' relation type. If for instance you have a product, which can have multiple images, you'll want a '**one-to-many**' relation type.

It is important to note that both types use the same `morphToMany` relation behind the scenes. It's only the UI which changes.


## <a name="one-to-one-relation" class="anchor" href="#one-to-one-relation"></a> One to one relation


Like the introduction said, this type of relation is for when you only need one file/image for a particular entity. In addition to this, the image can have a **zone** given. To stay consistent, using the Article module, example from the introduction, that cover image will have a zone of `coverimage`.

That way we can easily get the cover image for a particular article.

### MediaRelation trait

First thing you need is add the `Modules\Media\Support\Traits\MediaRelation` trait onto your desired *entity* (an eloquent model).

This will add a `files` morphToMany relation onto your entity.

From here you could already start implementing your own field to select a file from the media module, or you can include the partial.

### Include the partial

#### Create views

On create views you can follow the following easy steps:

- Insert the `media::admin.fields.new-file-link-multiple` partial like so:

``` php
@include('media::admin.fields.new-file-link-single', [
    'zone' => 'gallery'
])
```

- Trigger an event when you model was created
    - Your event needs to implement `Modules\Media\Contracts\StoringMedia`
    - Your event needs to have 1) the Entity and 2) the data from the form
    - The interface requires 2 methods, to return each of those properties

#### Edit views

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

### Getting the thumbnail from controller

The final step is to get the thumbnail from the controller so it can be displayed on the object if there is already a file linked to that object. If you're using the partial from the second step, this would be to display the linked image.

You can inject the `FileRepository` into your constructor or method and use the `findFileByZoneForEntity` method to get your image. This methods has two parameters, the zone name (*string*) and the entity (*object*) it needs to search on.

``` .language-php
$coverimage = $this->file->findFileByZoneForEntity('coverimage', $article);
```

One important note here is **the variable name has to be the same as the zone name**.


## <a name="one-to-many-relation" class="anchor" href="#one-to-many-relation"></a> One to many relation

This resembles very much the one-to-one relation, except the partial to include and the method to call to get all linked files.

### MediaRelation trait

First thing you need is add the `Modules\Media\Support\Traits\MediaRelation` trait onto your desired *entity* (eg: an eloquent model).

### Include the partial


#### Create views

On create views you can follow the following easy steps:

- Insert the `media::admin.fields.new-file-link-multiple` partial like so:

``` php
@include('media::admin.fields.new-file-link-multiple', [
    'zone' => 'gallery'
])
```

- Trigger an event when you model was created
    - Your event needs to implement `Modules\Media\Contracts\StoringMedia`
    - Your event needs to have 1) the Entity and 2) the data from the form
    - The interface requires 2 methods, to return each of those properties



#### Edit views

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

### Getting the thumbnails from controller

Now you can use the helper method on the `FileRepository` to fetch all files for the given object. It has also 2 parameters, the zone (*string*) and the entity (*object*) it needs to search on.

``` .language-php
$galleryFiles = $this->file->findMultipleFilesByZoneForEntity('gallery', $product);
```

Again, it is important **the variable name is the same as the zone name**.

## <a name="delete-polymorphic-relation" class="anchor" href="#delete-polymorphic-relation"></a> Deleting the polymorphic relation upon deletion of related model

Considering the example of a producting having images linked to it. When removing a product, we also want the polymorphic relation to be deleted (ie: the records in the `media__imageables` table). 

This can be accomplished by: 

- Trigger an event when you model was deleted
    - Your event needs to implement `Modules\Media\Contracts\DeletingMedia`
    - That event needs to have the id of the entity and its class name.
- Add the event class to the `asgard.media.events.deleting` configuration key.

That's it.