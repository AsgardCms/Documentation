# Modules Installation

## Core Module
This module is used for registering other modules Service Providers. It is also used for containing base classes.

* `php artisan module:install nWidart-Modules/Core`
* Add its Service Provider `'Modules\Core\Providers\CoreServiceProvider',` to your `config/app.php` file.

## Dashboard Module
The basic dashboard for your administration.

* `php artisan module:install nWidart-Modules/Dashboard`

## Session Module
This module will enable you to login into the admin dashboard. 

**Important**: you need to install Sentinel. And migrate and publish its configuration.

```
php artisan migrate --package=cartalyst/sentinel
php artisan publish:config cartalyst/sentinel
```

Change the `users` model key to:

``` json
'users' => [

	'model' => 'Modules\Session\Entities\User',

],
```

* `php artisan module:install nWidart-Modules/Session`
* Add the required Service Providers

  ``` php
  'Cartalyst\Sentinel\Laravel\SentinelServiceProvider',
  'Laracasts\Commander\CommanderServiceProvider',
  'Laracasts\Flash\FlashServiceProvider',
  ```
* Add the Aliases

  ``` php
  'Activation' => 'Cartalyst\Sentinel\Laravel\Facades\Activation',
  'Reminder' => 'Cartalyst\Sentinel\Laravel\Facades\Reminder',
  'Sentinel' => 'Cartalyst\Sentinel\Laravel\Facades\Sentinel',
  'Flash' => 'Laracasts\Flash\Flash',
  ```

## User Module
This module is used to handle your users, roles and permissions.

* `php artisan module:install nWidart-Modules/User`

## Workshop Module
This module lets you activate or deactivate modules. But also gives your a helper UI to generate new modules, install other modules and run some other commands.

* `php artisan module:install nWidart-Modules/Workshop`


***

[Back to ToC](../readme.md)