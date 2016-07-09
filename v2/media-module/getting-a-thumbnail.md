title: Getting thumbnails
subtitle: Media Module
-------

- [Injection](#injection)
- [Facade](#facade)

If you want to get a specific thumbnail of an image you can have 2 choices. Either you're in a view, then you'll use the Facade, if not use class/method injection.

## <a name="injection" class="anchor" href="#injection">Injection</a>

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


## <a name="facade" class="anchor" href="#facade">Facade</a>

In views, you can use the facade for ease of use. Simply send as first argument which image you want and which thumbnail:

``` .language-markup
<img src="{{ Imagy::getThumbnail('/assets/media/original-image-name.png', 'smallThumb') }}" alt="" />
```

