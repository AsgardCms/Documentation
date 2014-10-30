# Media Module: Getting a thumbnail

If you want to get a specific thumbnail of an image you can have 2 choices. Either you're in a view, then you'll use the Facade, if not use class/method injection.



## Injection

``` php
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
	$this->imagy->getThumbnail('/assets/media/original-image-name.png', 'smallThumb')
}

```


### Facade

``` html
<img src="{{ Modules\Media\Image\Facade\Imagy::getThumbnail('/assets/media/original-image-name.png', 'smallThumb') }}" alt="" />
```

If you don't want to use the fully qualified name, set the Imagy facade in your aliases key that can be found in `config/app.php`.

``` php
'Imagy' => 'Modules\Media\Image\Facade\Imagy'
```

Then afterwards you'll be able to use the following:

``` html
<img src="{{ Imagy::getThumbnail('/assets/media/original-image-name.png', 'smallThumb') }}" alt="" />
```


***

[Back to ToC](../readme.md)
