title: Permissions
subtitle: Core Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Authentication Contract](#authentication-contract)

### <a class="anchor" name="introduction" href="#introduction"></a> Introduction

In the same way the core listens for navigation items, it also listens for permissions. Your module can push the permissions it needs.

### <a class="anchor" name="usage" href="#usage"></a> Usage

All you have to do is have a `permissions.php` file in the modules Config file. This file will contain the permissions for your module.

Each module can define its permissions per *category*, prefixed by the singular module name. Take for instance the blog module:

``` .language-php
<?php

return [
    'blog.posts' => [
        'index',
        'create',
        'store',
        'edit',
        'update',
        'destroy'
    ],
    'blog.categories' => [
        'index',
        'create',
        'store',
        'edit',
        'update',
        'destroy'
    ],
    'blog.tags' => [
        'index',
        'create',
        'store',
        'edit',
        'update',
        'destroy'
    ],
];

```

That is all, the Core Module will loop over every configuration file and load them.

### <a class="anchor" name="authentication-contract" href="#authentication-contract"></a> Authentication contract

Once you've setup the appropriate roles with their permissions, you can start checking for them in controllers, views etc.

Do perform this action you can inject the [authentication contract](https://github.com/nWidart-Modules/Core/blob/master/Contracts/Authentication.php) which has a `hasAccess()` method. It has the following signature:

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
