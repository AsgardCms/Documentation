title: Permissions
subtitle: Core Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Authentication Contract](#authentication-contract)

## <a class="anchor" name="introduction" href="#introduction">Introduction</a>

In the same way the core listens for navigation items, it also listens for permissions. Your module can push the permissions it needs. This happens in a `permissions.php` configuration file.

## <a class="anchor" name="usage" href="#usage">Usage</a>

All you have to do is have a `permissions.php` file in the modules Config file. This file will contain the permissions for your module.

Each module can define its permissions per *category*, prefixed by the singular module name. Take for instance the blog module:

``` .language-php
<?php

'blog.posts' => [
    'index' => 'blog::post.list resource',
    'create' => 'blog::post.create resource',
    'edit' => 'blog::post.edit resource',
    'destroy' => 'blog::post.destroy resource',
],
'blog.categories' => [
    'index' => 'blog::category.list resource',
    'create' => 'blog::category.create resource',
    'edit' => 'blog::category.edit resource',
    'destroy' => 'blog::category.destroy resource',
],
'blog.tags' => [
    'index' => 'blog::tag.list resource',
    'create' => 'blog::tag.create resource',
    'edit' => 'blog::tag.edit resource',
    'destroy' => 'blog::tag.destroy resource',
],
```

That is all, the Core Module will loop over every configuration file and load them.

## <a class="anchor" name="authentication-contract" href="#authentication-contract">Authentication contract</a>

Once you've setup the appropriate roles with their permissions in the backend interface, you can start checking for them in controllers, views etc.

To perform this action you can inject the [authentication contract](https://github.com/nWidart-Modules/Core/blob/master/Contracts/Authentication.php) which has a `hasAccess()` method. It has the following signature:

``` .language-php
/**
 * Determines if the current user has access to given permission
 * @param $permission
 * @return bool
 */
public function hasAccess($permission);
```

An example, to check if a user has access to the users index page in the administration:

``` .language-php
$this->auth->hasAccess('users.index');
```

Which will return a boolean.

You can also call `hasAccess()` on a User model which implements the `UserInterface`contract.
