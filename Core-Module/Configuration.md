# Core module : Configuration

This **Core Module** has one main configuration item, you'll find it at `Modules/Core/Config/core.php`.

## Admin Prefix

With this configuration you can set how you access the admin dashboard. By default it is set to `backend`. Meaning you can access your admin dashboard on the following url `localhost:8000/backend` (if you're using the `artisan serve` command).

``` php
'admin-prefix' => 'backend'
```

***

[Back to ToC](../readme.md)