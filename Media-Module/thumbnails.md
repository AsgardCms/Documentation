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

### Crop

``` php
 'crop' => [
    'width' => '100', // required 
    'height' => '200', // required 
    'x' => 0 // optional
    'y' => 0 // optional
],
```

- **Width: ** [required] Width of the rectangular cutout.
- **Height: ** [required] Height of the rectangular cutout.
- **x: ** [optional] X-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.
- **y: ** [optional] Y-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.

### Fit

### Blur

### Brighten

