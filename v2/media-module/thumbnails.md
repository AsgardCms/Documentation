title: Thumbnails
subtitle: Media Module
-------

- [Basic Usage](#basic-usage)
- [Image quality](#image-quality)
- [Filters](#filters)

## <a name="basic-usage" class="anchor" href="#basic-usage">Basic usage</a>

You can define a set of thumbnails your site needs.

This can be done by using the `ThumbnailManager` interface and calling the `registerThumbnail()` on that.

Thumbnails are set by key and can have a set of attributes. For instance you could have a 'smallThumb' that crops the image and adds a blur filter. This is possible with this module.

For the example previously stated, you can call the following in your Module's Service Provider class in the `boot()` method:

``` .language-php
$this->app[ThumbnailManager::class]->registerThumbnail('smallThumb', [
    'resize' => [
        'width' => 50,
        'height' => null,
        'callback' => function ($constraint) {
            $constraint->aspectRatio();
            $constraint->upsize();
        },
    ],
]);
```

This will make the Media module aware of your thumbnails.

## <a name="image-quality" class="anchor" href="#image-quality">Image quality</a>

Each thumbnail can optionally also specify the image quality. This defaults to `90` and can be overwritten like so:

``` .language-php
$this->app[ThumbnailManager::class]->registerThumbnail('smallThumb', [
    'quality' => 60,
    'resize' => [
        'width' => 50,
        'height' => null,
        'callback' => function ($constraint) {
            $constraint->aspectRatio();
            $constraint->upsize();
        },
    ],
]);
```


## <a name="filters" class="anchor" href="#filters">Filters</a>

The filters use the [Intervention/Image](http://image.intervention.io/) library, almost all the filters it has can be used.

- [Crop](#crop)
- [Fit](#fit)
- [Blur](#blur)
- [Brightness](#brightness)
- [Colorize](#colorize)
- [Contrast](#contrast)
- [Flip](#flip)
- [Gamma](#gamma)
- [Greyscale](#greyscale)
- [Heighten](#heighten)
- [Invert](#invert)
- [LimitColors](#limitcolors)
- [Opacity](#opacity)
- [Orientate](#orientate)
- [Pixelate](#pixelate)
- [Resize](#resize)
- [Rotate](#rotate)
- [Sharpen](#sharpen)
- [Trim](#trim)
- [Widen](#widen)

### <a name="crop" class="anchor" href="#crop">Crop</a>

**Example**

``` .language-php
 'crop' => [
    'width' => '100', // required 
    'height' => '200', // required 
    'x' => 0 // optional
    'y' => 0 // optional
],
```

**Parameters**

- **Width:** [required] Width of the rectangular cutout.
- **Height:** [required] Height of the rectangular cutout.
- **x:** [optional] X-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.
- **y:** [optional] Y-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.

### <a name="fit" class="anchor" href="#fit">Fit</a>

**Example**

``` .language-php
'fit' => [
    'width' => '100',
    'height' => '200',
    'position' => 'top-left',
    'callback' => function($constraint) {
    	$constraint->upsize();
    }
],
```

**Parameters**

- **Width:** [required] The width the image will be resized to after cropping out the best fitting aspect ratio.
- **Height:** [optional] The height the image will be resized to after cropping out the best fitting aspect ratio. If no height is given, method will use same value as width.
- **position:** [optional] Set a position where cutout will be positioned. By default the best fitting aspect ration is centered.

    The possible values are:
    
    - top-left
	- top
	- top-right
	- left
	- center (default)
	- right
	- bottom-left
	- bottom
	- bottom-right
- **callback:** [optional] Closure callback defining constraint to prevent unwanted **upsizing** of the image.



### <a name="blur" class="anchor" href="#blur">Blur</a>

Apply a gaussian blur filter with a optional amount on the current image. Use values between `0` and `100`.

**Example**

``` .language-php
'blur' => [
    'amount' => '15'
],
```

**Parameters**

- **amount:** [optional] The amount of the blur strength. Use values between 0 and 100. Default: 1

### <a name="brightness" class="anchor" href="#brightness">Brightness</a>

Changes the brightness of the current image by the given level. Use values between `-100` for min. brightness `0` for no change and `+100` for max. brightness.

**Example**

``` .language-php
'brightness' => [
    'level' => '50'
],
```

**Parameters**

- **level:** [required] Level of brightness change applied to the current image. Use values between -100 and +100.

### <a name="colorize" class="anchor" href="#colorize">Colorize</a>

Change the RGB color values of the current image on the given channels **red**, **green** and **blue**. The input values are normalized so you have to include parameters from 100 for maximum color value `0` for no change and `-100` to take out all the certain color on the image.

**Example**

``` .language-php
'colorize' => [
    'red' => 0,
    'green' => 0,
    'blue' => 99
]
```

**Parameters**

- **red:** [required] Add or take out a amount of red color on the image. Use values between -100 and +100.
- **green:** [required] Add or take out a amount of green color on the image. Use values between -100 and +100.
- **blue:** [required] Add or take out a amount of blue color on the image. Use values between -100 and +100.


### <a name="contrast" class="anchor" href="#contrast">Contrast</a>

Changes the contrast of the current image by the given level. Use values between `-100` for min. contrast 0 for no change and `+100` for max. contrast.

**Example**

``` .language-php
'contrast' => [
    'level' => '50'
],
```

**Parameters**

- **level:** [required] Level of contrast change applied to the current image. Use values between -100 and +100.


### <a name="flip" class="anchor" href="#flip">Flip</a>

Mirror the current image horizontally or vertically by specifying the mode.

**Example**

``` .language-php
'flip' => [
    'mode' => 'h'
],
```

**Parameters**

- **mode:** [required] Specify the mode the image will be flipped. You can set h for horizontal (default) or v for vertical flip.

### <a name="gamma" class="anchor" href="#gamma">Gamma</a>

Performs a gamma correction operation on the current image.

**Example**

``` .language-php
'gamma' => [
    'correction' => '1.6'
],
```

**Parameters**

- **correction:** [required] Specify the mode the image will be flipped. You can set h for horizontal (default) or v for vertical flip.


### <a name="greyscale" class="anchor" href="#greyscale">Greyscale</a>

Turns image into a greyscale version.

**Example**

``` .language-php
'greyscale' => [],
```

**Parameters**

None


### <a name="heighten" class="anchor" href="#heighten">Heighten</a>

Resizes the current image to new **height**, constraining aspect ratio. Pass an optional Closure **callback** as third parameter, to apply additional constraints like preventing possible upsizing.

**Example**

``` .language-php
'heighten' => [
    'height' => '250'
    'callback' => function($constraint) {
    	$constraint->upsize();
    }
],
```

**Parameters**

- **height:** [required] The new height of the image
- **callback:** [optional] Closure callback defining constraint to prevent unwanted upsizing of the image.

### <a name="invert" class="anchor" href="#invert">Invert</a>

Reverses all colors of the current image.

**Example**

``` .language-php
'invert' => [],
```

**Parameters**

None

### <a name="limitcolors" class="anchor" href="#limitcolors">LimitColors</a>

Method converts the existing colors of the current image into a color table with a given maximum **count** of colors. The function preserves as much alpha channel information as possible and blends transparent pixels against a optional **matte color**.

**Example**

``` .language-php
'limitColors' => [
	'count' => 255,
	'matte' => '#ff9900'
],
```

**Parameters**

- **count:** [required] Maximum number of colors that should be retained in the color palette. Or `null` to convert to true color.
- **matte:** [optional] A color to blend transparent pixels against. Default: no matte color


### <a name="opacity" class="anchor" href="#opacity">Opacity</a>

Set the **opacity** in percent of the current image ranging from 100% for opaque and 0% for full transparency.

**Note: Performance intensive on larger images. Use with care.**

**Example**

``` .language-php
'opacity' => [
    'transparency' => '40'
],
```

**Parameters**

- **transparency:** [required] The new percent of transparency for the current image.

### <a name="orientate" class="anchor" href="#orientate">Orientate</a>

This method reads the EXIF image profile setting 'Orientation' and performs a rotation on the image to display the image correctly.


**Example**

``` .language-php
'orientate' => [],
```

**Parameters**

None


### <a name="pixelate" class="anchor" href="#pixelate">Pixelate</a>

Applies a pixelation effect to the current image with a given **size** of pixels.


**Example**

``` .language-php
'pixelate' => [
	'size' => 10
],
```

**Parameters**

- **size:** [required] Size of the pixels.


### <a name="resize" class="anchor" href="#resize">Resize</a>

Resizes current image based on given **width** and/or **height**. To constraint the resize command, pass an optional Closure **callback** as third parameter.


**Example**

``` .language-php
'resize' => [
	'width' => 100,
	'height' => 100,
	'callback' => function($constraint) {
		$constraint->aspectRatio();
	}
],
```

**Parameters**

- **width:** [required] The new width of the image
- **height:** [required] The new height of the image
- **callback:** [optional] Closure callback defining constraints on the resize. It's possible to constraint the **aspect-ratio** and/or a unwanted **upsizing** of the image. 


### <a name="rotate" class="anchor" href="#rotate">Rotate</a>

Rotate the current image counter-clockwise by a given **angle**. Optionally define a **background color** for the uncovered zone after the rotation.


**Example**

``` .language-php
'rotate' => [
	'angle' => -45,
	'bgcolor' => '#000000',
],
```

**Parameters**

- **angle:** [required] The rotation angle in degrees to rotate the image counter-clockwise.
- **bgcolor:** [required] A background color for the uncovered zone after the rotation. Default: `#000000`


### <a name="sharpen" class="anchor" href="#sharpen">Sharpen</a>

Sharpen current image with an optional **amount**. Use values between `0` and `100`.


**Example**

``` .language-php
'sharpen' => [
	'amount' => 10
],
```

**Parameters**

- **amount:** [optional] The amount of the sharpening strength. Method accepts values between `0` and `100`. Default: `10`


### <a name="trim" class="anchor" href="#trim">Trim</a>

Trim away image space in given color. Define an optional **base** to pick a color at a certain position and borders that should be trimmed **away**. You can also set an optional **tolerance** level, to trim similar colors and add a **feathering** border around the trimmed image.

**Note: Resource intensive with GD driver. Use with care.**


**Example**

``` .language-php
'trim' => [
	'base' => 'top-left',
	'away' => 'top',
	'tolerance' => 0,
	'feather' => 0,
],
```

**Parameters**

- **base:** [required] Define the the point from where the trimming color is picked. For example if you set this parameter to bottom-right, all color will be trimmed away that is equal to the color in the bottom-left corner of the image.
   
   Possible values are:
   
   - top-left (default)
   - bottom-right
   - transparent
- **away:** [optional] Border(s) that should be trimmed away. You can add multiple borders. as an array of values. 

   Possible values are:
   
   - top
   - bottom
   - left
   - right
   
   By default the trimming is performed on all borders.

- **tolerance:** [optional] Define a percentaged tolerance level between `0` and `100` to trim away similar color values. Default: `0`
- **feather:** [optional] Sometimes it may be useful to leave a untouched "border" around an object while trimming. Especially when trimming non-solid backgrounds you can expand (positive value) or contract (negative value) the space around the trimmed object by a certain amount of pixels. Default: `0`


### <a name="widen" class="anchor" href="#widen">Widen</a>

Resizes the current image to new **width**, constraining aspect ratio. Pass an optional Closure **callback** as third parameter, to apply additional constraints like preventing possible upsizing.

**Example**

``` .language-php
'heighten' => [
    'width' => '250'
    'callback' => function($constraint) {
    	$constraint->upsize();
    }
],
```

**Parameters**

- **width:** [required] The new width of the image
- **callback:** [optional] Closure callback defining constraint to prevent unwanted upsizing of the image.
