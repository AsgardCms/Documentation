title: Configuration
subtitle: Media Module
-------

- [Filesytem](#filesystem)
- [Media assets path](#media-assets-path)
- [Allowed types](#allowed-types)
- [Max file size](#max-file-size)
- [Max total size](#max-total-size)

The **Media module** configuration file can be found at `config/asgard.media.config.php`.

## <a class="anchor" name="filesystem" href="#filesystem"></a> Filesystem

Define the filesystem you would like to use to store the media. Currently only disk and s3 are supported. 

Feel free to an [UrlResolver](https://github.com/AsgardCms/Media/blob/master/UrlResolvers/BaseUrlResolver.php) for your desired filesystem as a pull request.

``` .language-php
'filesystem' => 'local',
```

## <a class="anchor" name="media-assets-path" href="#media-assets-path"></a> Media assets path


This is the path where the media files will be uploaded.

It defaults to `/assets/media/`.

``` .language-php
'files-path' => '/assets/media/',
```

## <a class="anchor" name="allowed-types" href="#allowed-types"></a> Allowed types

Specify all the allowed file extensions a user can upload on the server.

It defaults to `.jpg,.png`.

``` .language-php
'allowed-types' => '.jpg,.png',
```

## <a class="anchor" name="max-file-size" href="#max-file-size"></a> Max file size

Determine the max file size upload rate, defined in **mb**.

It defaults to **5mb**.

``` .language-php
'max-file-size' => '5',
```

## <a class="anchor" name="max-total-size" href="#max-total-size"></a> Max total size

Determine the max total media folder size, expressed in bytes.

It defaults to **1000000000 bytes** (1gb).

``` .language-php
'max-total-size' => 1000000000,
```
