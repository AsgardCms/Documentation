title: Installation
subtitle: Getting Started
-------

- [Minimum System Requirements](#minimum-system-requirements)
- [Install AsgardCMS](#install-asgardcms)

### <a name="minimum-system-requirements" class="anchor" href="#minimum-system-requirements"></a> Minimum System Requirements

To be able to run AsgardCMS you have to meet the following requirements:

- PHP 5.5.9 or higher
- PDO PHP Extension
- cURL PHP Extension
- OpenSSL PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- GD PHP Library
- MySql 5.5
- One of the following cache drivers: `memcached`, `redis`, `apc`. (defaults to `array`)

### <a name="install-asgardcms" class="anchor" href="#install-asgardcms"></a> Install AsgardCMS

If you prefer a video to see how the installation process goes, [watch the install video](https://www.youtube.com/watch?v=MeX_D-aql6g).


#### Get AsgardCMS

``` .language-bash
composer create-project asgardcms/platform your-project-name
```

#### Create a database

#### Intall your prefered user system

- Sentry (installed by default)
- Sentinel (run `composer update` if you choose Sentinel)
	- add `"cartalyst/sentinel": "~2.0"`
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

You can now login on `/auth/login` with your email and password asked during the install command. After you've logged in you'll be able to access the administration panel on the `/backend` URI.

#### Feedback, ideas, etc.
If you have **feedback** to give, **ideas** you would like implemented, by all means share them on the [dedicated uservoice page](http://asgardcms.uservoice.com/). Do not hesitate to share! 

For **issues/bugs** your having, you can use the Github Issues to post those. All issues are grouped on the [AsgardCms/Platform](https://github.com/AsgardCms/Platform/issues) repository.

If you just want to **talk**, join [our Slack channel](http://slack.asgardcms.com/).

Thank you for your participation!