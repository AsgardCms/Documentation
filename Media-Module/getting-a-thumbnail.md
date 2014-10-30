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
<img src="{{ Imagy::getThumbnail('/assets/media/original-image-name.png') }}" alt="" />
```

***

[Back to ToC](../readme.md)
