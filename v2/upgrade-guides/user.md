title: Upgrade Guide
subtitle: User module
-------

- [From v1 to v2](#upgrade-2.0)
- [From 1.13.1 to 1.14.0](#upgrade-1.14.0)
- [From 1.11.0 to 1.12.0](#upgrade-1.12.0)



## <a name="upgrade-2.0" class="anchor" href="#upgrade-2.0">From v1 to **v2**</a>

**[> Changelog](https://github.com/AsgardCms/User/blob/2.0/changelog.yml)**

**Authentication contract changes**

The interface itself has changed namespace:

- From : `Modules\Core\Contracts\Authentication`
- To: `Modules\User\Contracts\Authentication`

The `check()` method has changed signature. 

- Previous behaviour: it returned `false` if no user logged in, or the logged in user, if logged in.
- New behaviour: it returns `false` if not logged in, `true` if logged in.

To get the current logged in user, there's a new method added: `user()`.


**Acessing the currently logged in user**

The currently logged in user is now loaded on every view by default.

You can access the currently logged in user with the `$currentUser` variable.

**New permissions middleware**

Before in AsgardCMS v1 permissions where checked by reading the current URI and matching that with the keys in the `permissions.php` config file of every module.

This worked but wasn't very flexible and thus been removed on AsgardCMS v2.

There is a new `Authorization` middleware class which can be used as displayed:

``` .language-php
$router->get('users', [
    'as' => 'admin.user.user.index',
    'uses' => 'UserController@index',
    'middleware' => 'can:user.users.index',
]);
```

The value after `can:` is the corresponding key in your `permissions.php` file.

**`users.php` config file rename**

the `users.php` configuration file was renamed to `config.php` in the User module.

This mean if you used those configuration items in your modules you need to replace:

- `config('asgard.user.users`
- by: `config('asgard.user.config`


## <a name="upgrade-1.14.0" class="anchor" href="#upgrade-1.14.0">From 1.13.1 to **1.14.0**</a>

**Translations have been removed**

All translations files were removed from the individual modules and moved to the [Translation](https://github.com/AsgardCms/Translation) module. Therefore you will need to require the Translation module in your project. This can be done by running the following command in your project:

``` .language-bash
composer require asgardcms/translation-module
```

## <a name="upgrade-1.12.0" class="anchor" href="#upgrade-1.12.0">From 1.11.0 to **1.12.0**</a>

**New authentication views**

All authentication views were updated to the latest version of AdminLTE. If you were using the default authentication views and had them published, you will need to re-publish those views. This can be done with the following command:

``` .language-bash
php artisan vendor:publish --provider="Modules\User\Providers\UserServiceProvider" --force
```

