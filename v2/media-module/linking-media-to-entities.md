title: Linking media to Entities
subtitle: Media Module
-------

- [Adding the `MediaRelation` trait](#adding-media-relation-trait)
- [Display input on your views](#display-input-on-views)
- [Trigger event on create/update](#trigger-event)
- [Deleting the polymorphic relation upon deletion of related model](#delete-polymorphic-relation)

You can use the media uploaded in any module you make. 

Lets say you have an articles module, and want your article to have a *cover image*. This is when you'll want a '**one-to-one**' relation type. If for instance you have a product, which can have multiple images (a *gallery*), you'll want a '**one-to-many**' relation type.

In this example, *cover_image* and *gallery* are what we call "zones". Zones are basically groups of files, which allows us to get all (or one) file(s) for a specific group, for an entity.

Zones can be imagined as part of website pages, to which we assign files.

It is important to note that both types use the same `morphToMany` relation behind the scenes. It's only the UI which changes.


## <a name="adding-media-relation-trait" class="anchor" href="#adding-media-relation-trait">1. Adding the `MediaRelation` trait</a>

First thing you need is add the `Modules\Media\Support\Traits\MediaRelation` trait onto your desired *entity* (an eloquent model).

This will add a `files` morphToMany relation onto your entity.


## <a name="display-input-on-views" class="anchor" href="#display-input-on-views">2. Display input on your views</a>


### One to One (one file)

This is if you want to include a single file for a given `zone`, like for example a `feature_image`.

- The first argument is the name of the zone.
- (optional) Second argument is the entity to store the media for.
- (optional) Third argument can be a view to use. This will override the default media view with its input field.
- (optional) Fourth and last argument can be a name to use. This will override the default name for the input field.

Simple include the following blade directive:

``` .language-php
// Create view
@mediaSingle('featured_image')

// Edit view
@mediaSingle('featured_image', $article)
```

### One to Many (multiple files)

This is if you want to include multiple files for a given `zone`, like for example a gallery of images. Those images can also be re-ordered.

- The first argument is the name of the zone.
- (optional) Second argument is the entity to store the media for.
- (optional) Third argument can be a view to use. This will override the default media view with its input field.
- (optional) Fourth and last argument can be a name to use. This will override the default name for the input field.

``` .language-php
// Create view
@mediaMultiple('gallery')

// Edit view
@mediaMultiple('gallery', $article)
```

## <a name="trigger-event" class="anchor" href="#trigger-event">3. Trigger event on create/update</a>

These events will let the media module know it needs to handle the data from the form to link / unlink files.

You will need to trigger an event in your repository, when the entity was created and when it was updated. Both events will need the following:

- Implement the `Modules\Media\Contracts\StoringMedia` interface
- Needs to have 1) the Entity and 2) the data from the form
- The interface requires 2 methods, to return each of those properties

This is an *example* of one of those events:

``` .language-php
class RecipeWasCreated implements StoringMedia
{
    private $recipe;
    private $data;

    public function __construct($recipe, $data)
    {
        $this->recipe = $recipe;
        $this->data = $data;
    }

    /**
     * Return the entity
     * @return \Illuminate\Database\Eloquent\Model
     */
    public function getEntity()
    {
        return $this->recipe;
    }

    /**
     * Return the ALL data sent
     * @return array
     */
    public function getSubmissionData()
    {
        return $this->data;
    }
}
```

## <a name="delete-polymorphic-relation" class="anchor" href="#delete-polymorphic-relation">4. Deleting the polymorphic relation upon deletion of related model</a>

Considering the example of a product having images linked to it. When removing a product, we also want the polymorphic relation to be deleted (ie: the records in the `media__imageables` table). 

This can be accomplished by: 

- Trigger an event when you model was deleted
    - Your event needs to implement `Modules\Media\Contracts\DeletingMedia`
    - That event needs to have the id of the entity and its class name.

That's it.
