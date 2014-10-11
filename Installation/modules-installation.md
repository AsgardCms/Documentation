# Modules Installation

## Core Module
This module is used for registering other modules Service Providers. It is also used for containing base classes. 

* `php artisan module:install nWidart-Modules/Core`
* Add its Service Provider `'Modules\Core\Providers\CoreServiceProvider',` to your `config/app.php` file.
* Add the required Service Providers

  ``` php
  'Cartalyst\Sentinel\Laravel\SentinelServiceProvider',
  'Laracasts\Commander\CommanderServiceProvider',
  'Laracasts\Flash\FlashServiceProvider',
  'Mcamara\LaravelLocalization\LaravelLocalizationServiceProvider',
  ```
* Add the Aliases

  ``` php
  'Activation' => 'Cartalyst\Sentinel\Laravel\Facades\Activation',
  'Reminder' => 'Cartalyst\Sentinel\Laravel\Facades\Reminder',
  'Sentinel' => 'Cartalyst\Sentinel\Laravel\Facades\Sentinel',
  'Flash' => 'Laracasts\Flash\Flash',
  'LaravelLocalization' => 'Mcamara\LaravelLocalization\Facades\LaravelLocalization',
   ```
   
If you installed the module manually, this is what your composer.json needs:

```
"cartalyst/sentinel": "1.0.*",
"laracasts/commander": "dev-master",
"laracasts/flash": "~1.0",
"laracasts/presenter": "0.2.*",
"guzzlehttp/guzzle": "4.2.2",
"mcamara/laravel-localization": "dev-Laravel5Support",
"dimsav/laravel-translatable": "dev-laravel-5"
```

## Dashboard Module
The basic dashboard for your administration.

* `php artisan module:install nWidart-Modules/Dashboard`

## User Module

This module will enable you to login into the admin dashboard and handle your users, roles and permissions.

**Important**: you need to install Sentinel. And migrate and publish its configuration.

```
php artisan migrate --package=cartalyst/sentinel
php artisan publish:config cartalyst/sentinel
```

Change the `users` model key to:

``` json
'users' => [

	'model' => 'Modules\User\Entities\User',

],
```

* `php artisan module:install nWidart-Modules/User`




## Workshop Module
This module lets you activate or deactivate modules. But also gives your a helper UI to generate new modules, install other modules and run some other commands.

* `php artisan module:install nWidart-Modules/Workshop`


Now that you have to Workshop module installed you can use the GUI to install other modules.

***

[Back to ToC](../readme.md)