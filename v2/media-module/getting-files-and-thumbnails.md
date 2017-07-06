title: Getting files and thumbnails
subtitle: Media Module
-------

- [Getting files](#getting-files)
- [Getting thumbnails](#getting-thumbnails)



## <a name="getting-files" class="anchor" href="#getting-files">Getting files</a>

Thanks to the `MediaRelation` trait it's easy to find the files linked to your entities.

The `MediaRelation` trait has 2 main methods for you to leverage. `files()` and `filesByZone()`. Both are a morphToMany relation, the second being easier to use to day to day usage.

Let's say you have products, that have a featured images. You want an easy way to grab those images. The long way would be something like this:

```.language-php
// In a controller
$images = $product->files()->where('zone', 'featured_images')->get();
// Same as
$images = $product->filesByZone('featured_images')->get();
```

This is find, but isn't really pretty to use in views. To avoid this issue, we can leverage laravel's [accessor feature](https://laravel.com/docs/5.4/eloquent-mutators). Let's add one on our `Product` entity.

```.language-php
class Product extends Model
{
    public function getFeaturedImagesAttribute()
    {
        return $this->filesByZone('featured_images')->get();
    }
}
```

With this you can now call this as an attribute: `$product->featured_images`.

Of course, this is not limited to images, but any type of file. This can also be a single file, by using `first()` instead of `get()`;

### MediaPath

`MediaPath` is a value object that will be returned when you get a file from the previous methods. Usually you won't even notice. 

We want to display our product images:

```.language-php
// In a blade view
@foreach($products as $product)
    @foreach($product->featured_images as $featuredImage)
        <img src="{{ $featuredImage->path }}" alt=""/>
    @endforeach
@endforeach
```

If a product had a single file, lets say a specification pdf:

```.language-markup
<a href="{{ $product->specification_pdf->path }}">Download pdf</a>
```



## <a name="getting-thumbnails" class="anchor" href="#getting-thumbnails">Getting thumbnails</a>


If you want to get a specific thumbnail of an image you can have 2 choices. Either you're in a view, then you'll use the Facade, if not use class/method injection.

### Facade

In views, you can use the facade for ease of use. Simply send as first argument which image you want and which thumbnail:

``` .language-markup
<img src="{{ Imagy::getThumbnail('/assets/media/original-image-name.png', 'smallThumb') }}" alt="" />
```

Of course, your paths will usually not be referenced to manually but rather coming from an entity:


``` .language-markup
<img src="{{ Imagy::getThumbnail($product->featured_image->path, 'smallThumb') }}" alt="" />
```



### Dependency injection

``` .language-php
/**
 * @var Imagy
 */
private $imagy;

public function __construct(Imagy $imagy)
{
    $this->imagy = $imagy;
}

public function index()
{
	$thumbnail = $this->imagy->getThumbnail('/assets/media/original-image-name.png', 'smallThumb');
}
```


