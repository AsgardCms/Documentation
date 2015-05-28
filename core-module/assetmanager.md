title: Asset Manager
subtitle: Core Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Using in own Theme](#custom-theme)


### <a class="anchor" name="introduction" href="#introduction"></a> Introduction

The asset manager in AsgardCms is a helper to let you load assets faster without making you look at the filesystem to find assets. It is important to note that the asset manager is not a requirement, you can choose not to use it if you wish.

### <a class="anchor" name="usage" href="#usage"></a> Usage


Asgard Asset Manager is a 2 part package. First there is the **manager** in which you add *all* the assets you will need to build your site. This doesn't mean those assets will be included in all files, it merely means they will be ready for the **asset pipeline** to require them on the page.


#### Asset Manager


You can add assets on the manager using two different ways:

First and easiest way is to add assets in the `config/asgard.core.core.php` config file, in the `admin-assets` key. Those will be added onto the manager.

The second way is to manually calling the `AssetManager` in a class somewhere. You can do this by injecting the `Modules\Core\Foundation\Asset\Manager\AssetManager` interface and using the following methods:

``` .language-php
/**
 * Add a possible asset
 * @param string $dependency
 * @param string $path
 * @return void
 */
public function addAsset($dependency, $path);

/**
 * Add an array of possible assets
 * @param array $assets
 * @return void
 */
public function addAssets(array $assets);
```

As you can see you can either pass a dependency name and its path to `addAsset`, or by sending an array to `addAssets`. That array needs to have as key the dependency name and value the path to that dependency.


#### Asset Pipeline

After adding all possible dependencies on the asset manager, you are ready to require them on a page.

As you might already have seen, in the `config/asgard.core.core.php` file there is a `admin-required-assets` (which calls all assets by its name defined on the asset manager). This key sets all default assets that will **always** be included on the AdminLTE theme.

If a particular view needs a couple more assets, you can define those in the controller method that handles that view.

For instance a Page Edit view, needs CkEditor and a css file for the iCheck jQuery plugin. Those are not loaded on every view.

To add them onto the view I call these methods to require those assets:

``` .language-php
$this->assetPipeline->requireJs('ckeditor.js');
$this->assetPipeline->requireCss('icheck.blue.css');
```
Remember that those key names `ckeditor.js` and `icheck.blue.css` are the dependency names used in the Asset Manager.

Those 2 lines will add these assets on the desired view, that is all.

If you're in an Admin Controller, you have access to the `assetPipeline` and `assetManager` properties simply by extending the `Modules\Core\Http\Controllers\Admin\AdminBaseController` Controller.

##### Before and After

The asset pipeline also enables you to add an asset at a specific position on the pipeline. Let's say for instance that your javascript plugin requires jQuery, you can call the asset pipeline like so:

``` .language-php
$this->assetPipeline->requireJs('jquery-plugin')->after('jquery');
```

Or if you need it to load before a certain other asset:

``` .language-php
$this->assetPipeline->requireJs('jquery-plugin')->before('bootstrap');
```

Those methods are of course also available for css assets.



### <a class="anchor" name="custom-theme" href="#custom-theme"></a> Using in own Theme


If you're on a custom admin or front end theme, you can create a view composer that will add the `cssFiles` and `jsFiles` variables onto the views.

The `MasterViewComposer` in the Core module does this the following way:

``` .language-php
$view->with('cssFiles', $this->assetPipeline->allCss());
$view->with('jsFiles', $this->assetPipeline->allJs());
```

Now in the master layout of the AdminLTE template you can simply loop over those assets:

``` .language-php
@foreach($cssFiles as $css)
    <link media="all" type="text/css" rel="stylesheet" href="{{ $css }}">
@endforeach
```

and :

``` .language-php
@foreach($jsFiles as $js)
    <script src="{{ $js }}" type="text/javascript"></script>
@endforeach
```

