title: Upgrade Guide
subtitle: Core module
-------

- [From v1 to v2](#upgrade-2.0)


## <a name="upgrade-2.0" class="anchor" href="#upgrade-2.0">From v1 to **v2**</a>

**[> Changelog](https://github.com/AsgardCms/Core/blob/2.0/changelog.yml)**

**Re-problish configuration files**

Configuration files across modules has been changed, mostly the `permissions.php` files.

Using the following command you will be able to publish a module config files.

``` .language-bash
php artisan module:publish-config --force
```

If you edited the module configurations, you will need to manually copy over the new files, depending on what you changed, you can also publish each module individually.

**Each module needs to handle config file loading**

Previously the Core module did the configuration loading for every module. This responsability has now been moved to every individual module. The reason is to have more flexibility on publishing modules configuration.

To register your configuration files, you can use a helper trait `CanPublishConfiguration`, with the `publishConfig($moduleName, $filename)` method. It takes the module name as first argument and the filename without extension as second.

**Namespace change of Authentication and Setting interfaces**

The Interface following interfaces that were previously under de Core namespace have been moved:

- From : `Modules\Core\Contracts\Authentication`
- To: `Modules\User\Contracts\Authentication`

- From: `Modules\Core\Contracts\Setting`
- To: `Modules\Setting\Contracts\Setting`

**Permission config file structure changes**

The permssions system has been revamped in v2. On top of the UI changes, which has changed to display a way to inherit permissions. The permissions now also display a `label`.

This `label` is more user-friendly than the previous `index`, `create` etc permission names.

In order to update your permissions to allow this you need to add the perrmisions in a `key -> value` structure. 

Example:

``` .language-php
'blog.posts' => [
    'index' => 'blog::post.list resource',
    'create' => 'blog::post.create resource',
    'edit' => 'blog::post.edit resource',
    'destroy' => 'blog::post.destroy resource',
],
```

The key is what we previously had in v1, and the value is a **translation key** of the label. This label will be display in the permissions listing UI.


**`MasterViewComposer` name has changed**

If you were using the `MasterViewComposer` class its name has been changed:

- From: `Modules\Core\Composers\MasterViewComposer`
- To: `Modules\Core\Composers\SiteNameViewComposer`

**Acessing the currently logged in user**

The currently logged in user is now loaded on every view by default.

You can access the currently logged in user with the `$currentUser` variable.

**`laracast\Flash` dependency has been removed**

Replace usages of `flash()` by adding it on the `view()` helper.

Example:

*Before:*

``` .language-php
flash(trans('blog::messages.category created'));

return redirect()->route('admin.blog.category.index')
```

*Now:*

``` .language-php
return redirect()->route('admin.blog.category.index')
            ->withSuccess(trans('blog::messages.category created')
```

**`Pingpong\modules` dependency has been replaced by `nwidart\laravel-modules`**

This is only relevant if you used any classes under he `Pingpong\Modules` namespace.

If you did use them replace:

- `Pingpong\Modules`
- by: `Nwidart\Modules`

**Google Analytics setting name change**

The previously called setting name `core::google-analytics`, has been renamed to `core::analytics-script`.

Update your database to match the new keyname, or re-save the settings.