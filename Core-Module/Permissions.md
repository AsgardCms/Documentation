# Core module : Permissions


## Introduction

In the same way the core listens for navigation items, it also listens for permissions. Your module can push the permissions it needs.

## Usage

All you have to do is have a `permissions.php` file in the modules Config file. This file will contain the permissions for your module.

Each module can define its permissions per *category*. Take for instance the blog module:

```php
<?php

return [
    'posts' => [
        'index',
        'create',
        'store',
        'edit',
        'update',
        'destroy'
    ],
    'categories' => [
        'index',
        'create',
        'store',
        'edit',
        'update',
        'destroy'
    ],
    'tags' => [
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