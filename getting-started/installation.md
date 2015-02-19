title: Installation
subtitle: Getting Started
-------

- [While in beta](#while-in-beta)
- [Minimum System Requirements](#minimum-system-requirements)
- [Install AsgardCMS](#install-asgardcms)

### <a name="minimum-system-requirements" class="anchor" href="#minimum-system-requirements"></a> Minimum System Requirements

To be able to run AsgardCMS you have to meet the following requirements:

- PHP 5.4 or higher
- PDO PHP Extension
- cURL PHP Extension
- MCrypt PHP Extension
- GD PHP Library
- One of the following cache drivers: memcached, redis, apc

### <a name="while-in-beta" class="anchor" href="#while-in-beta"></a> While in beta:

**While AsgardCMS is in its beta period the below installation won't be available.**

- Clone the [AsgardCMS repository](https://github.com/AsgardCms/Platform) manually
- Install your prefered user package, either Sentinel ou Sentry,
	- Sentinel :
		- add `"cartalyst/sentinel": "dev-feature/laravel-5"`
		- Add the Service Provider and aliases
	- Sentry (default already installed): 
		- add `"cartalyst/sentry": "dev-feature/laravel-5",`
		- Add the Service Provider and aliases
- Run `composer install`,
- Run `php artisan asgard:install` to start the installation process.


#### Feedback, ideas, etc.
If you have **feedback** to give, **ideas** you would like implemented, by all means share them on the [dedicated uservoice page](http://asgardcms.uservoice.com/). Do not hesitate to share! If you feel like talking, you can join the IRC channel at #asgardcms on freenode.

For **issues/bugs** your having, you can use the Github Issues to post those. Each module has its own repository on the [AsgardCMS](https://github.com/AsgardCms) organisation, find the one that gives you problems, and sumbit an issue.

Thank you for your participation!

### <a name="install-asgardcms" class="anchor" href="#install-asgardcms"></a> Install AsgardCMS

#### Get AsgardCMS

``` .language-bash
composer create-project asgardcms/platform your-project-name --prefer-dist --stability=dev
```

#### Run composer install

Run the usual `composer install` to get the dependencies.

#### Intall your prefered user system

- Sentinel
	- add `"cartalyst/sentinel": "dev-feature/laravel-5"`
	- Add the Service Provider and aliases
- Sentry (installed by default): 
	- add `"cartalyst/sentry": "dev-feature/laravel-5",`
	- Add the Service Provider and aliases



#### Run the install command

Now run `php artisan asgard:install` command to perform to start the installation process.

This install command will perform the following actions:

- Setup database information
- Running migrations
- Running seeds
- Publishing assets
- Create a first admin account


### Enjoy

You can now login on `/auth/login` with your email and password asked during the install command. After you've logged in you'll be able to access the administration panel on `/backend`.
