# Media Module: Thumbnails


## Basic usage

You can define a set of thumbnails your site needs.

This can be done by adding thumbnails to a settings file located at `Modules\Media\Config\thumbnails.php`.

Thumbnails are set by key and can have a set of attributes. For instance you could have a 'smallThumb' that crops the image and adds a blur filter. This is possible with this modules.

For the example previously stated, the thumbnail settings file can start like this:

``` php
return [
    'smallThumb' => [
        'crop' => [
            'width' => '100',
            'height' => '200'
        ],
        'blur' => [
            'amount' => '15'
        ],
    ]
];
```

## Filters

The filters use the [Intervention/Image](http://image.intervention.io/) library, almost all the filters it has can be used.

- [Crop](#crop)
- [Fit](#fit)
- [Blur](#blur)
- [Brightness](#brightness)
- [Colorize](#colorize)
- [Contrast](#contrast)


### Crop

#### Example

``` php
 'crop' => [
    'width' => '100', // required 
    'height' => '200', // required 
    'x' => 0 // optional
    'y' => 0 // optional
],
```

#### Parameters

- **Width:** [required] Width of the rectangular cutout.
- **Height:** [required] Height of the rectangular cutout.
- **x:** [optional] X-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.
- **y:** [optional] Y-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.

### Fit

#### Example

``` php
'fit' => [
    'width' => '100',
    'height' => '200',
    'position' => 'top-left'
],
```

#### Parameters

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

### Blur

#### Example

``` php
'blur' => [
    'amount' => '15'
],
```

#### Parameters

- **amount:** [optional] The amount of the blur strength. Use values between 0 and 100. Default: 1

### Brightness

#### Example

``` php
'brightness' => [
    'level' => '50'
],
```

#### Parameters

- **level:** [required] Level of brightness change applied to the current image. Use values between -100 and +100.

### Colorize

#### Example

``` php
'colorize' => [
    'red' => 0,
    'green' => 0,
    'blue' => 99
]
```

#### Parameters

- **red:** [required] Add or take out a amount of red color on the image. Use values between -100 and +100.
- **green:** [required] Add or take out a amount of green color on the image. Use values between -100 and +100.
- **blue:** [required] Add or take out a amount of blue color on the image. Use values between -100 and +100.


### Contrast

#### Example

``` php
'contrast' => [
    'level' => '50'
],
```

#### Parameters

- **level:** [required] Level of contrast change applied to the current image. Use values between -100 and +100.

