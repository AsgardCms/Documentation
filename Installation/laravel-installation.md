# Laravel Installation

Let's start of by installer the laravel framework, specificaly the laravel 5 (hence the `-b develop` flag).

```
git clone -b develop https://github.com/laravel/laravel.git yourProjectName
```

## Install Illuminate/Html

Add `"illuminate/html": "~5.0",` to your require key in `composer.json`.
Next add the service provider : 


``` php
'Illuminate\Html\HtmlServiceProvider',
```

And the Alias:

``` php
'Form' => 'Illuminate\Html\FormFacade',
```


## Install Pingpong/Modules

Install the [Pingpong/Modules](https://github.com/pingpong-labs/modules) package.

### Installation

Open your composer.json file and add a new required package.

  ```
  "pingpong/modules": "1.*"
  ```

Next, open a terminal and run.

  ```
  composer update 
  ```
  
Next, Add new service provider in `app/config/app.php`.

  ``` php
  'Pingpong\Modules\ModulesServiceProvider',
  ```
  
Next, Add new class alias in `app/config/php`.

  ``` php
  'Module'        => 'Pingpong\Modules\Facades\Module',
  ```
  
Next, publish package configuration. Open your terminal and run:

  ```
  php artisan config:publish pingpong/modules
  ```

Done.

### Setup modules folder for first use

By default modules folder is in your `app/` directory. For first use, please run this command on your terminal.
  ```
  php artisan module:setup
  ```

## Install i18n packages

Intall the [mcamara/laravel-localization](https://github.com/mcamara/laravel-localization) package.

### Installation

Add Laravel Localization to your `composer.json` file.

    "mcamara/laravel-localization": "0.14.*"

Run `composer install` to get the latest version of the package.

If you are using a laravel version lower than 4.2, you should use 0.13.* version.


### Laravel 4

Laravel Localization comes with a service provider for Laravel 4. You'll need to add it to your `composer.json` as mentioned in the above steps, then register the service provider with your application.

Open `app/config/app.php` and find the `providers` key. Add `LaravelLocalizationServiceProvider` to the array.

``` php
	...
	'Mcamara\LaravelLocalization\LaravelLocalizationServiceProvider'
	...
```

You can also add an alias to the list of class aliases in the same app.php

``` php
	...
	'LaravelLocalization'	=> 'Mcamara\LaravelLocalization\Facades\LaravelLocalization'
	...
```

To finish, publish the configuration file using the command `php artisan config:publish mcamara/laravel-localization` in your laravel root path. This will create the following file `app/config/packages/mcamara/laravel-localization/config.php`, containing the most common setting options.


***

[Back to ToC](../readme/md)