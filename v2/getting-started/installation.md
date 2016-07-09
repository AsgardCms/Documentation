title: Installation
subtitle: Getting Started
-------

- [Minimum System Requirements](#minimum-system-requirements)
- [Install AsgardCMS](#install-asgardcms)
- [Getting help](#getting-help)

## <a name="minimum-system-requirements" class="anchor" href="#minimum-system-requirements">Minimum System Requirements</a>

To be able to run AsgardCMS you have to meet the following requirements:

- PHP 5.6 or higher
- PDO PHP Extension
- cURL PHP Extension
- OpenSSL PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- Mcrypt PHP Extension
- GD PHP Library
- MySql 5.5
- One of the following cache drivers: `memcached`, `redis`, `apc`. (defaults to `array`)

## <a name="install-asgardcms" class="anchor" href="#install-asgardcms">Install AsgardCMS</a>

If you prefer a video to see how the installation process goes, [watch the install video](https://www.youtube.com/watch?v=MeX_D-aql6g).


### Get AsgardCMS

``` .language-bash
composer create-project asgardcms/platform=2.0.x-dev your-project-name
```

### Create a database

Create a database suiting your preferred method, Sequel Pro, MySQL Workbench, cli, however you prefer. Remember the database name you used as this well be asked in the installation command.

### Install your preferred user system

- Sentinel (installed by default) 

More user implementations may be offered later on. Learn how you can add your custom [ACL implementations](v2/user-module/drivers.md).


### Run the install command

Now run `php artisan asgard:install` command to perform the installation process.

This install command will perform the following actions:

- Setup database information
- Running migrations
- Running seeds
- Publishing assets
- Create a first admin account


### Enjoy

You can now login on `/auth/login` with your email and password asked during the install command. After you've logged in you'll be able to access the administration panel on the `/backend` URI.


## <a name="getting-help" class="anchor" href="#getting-help">Getting help</a>

If you have **feedback** to give, **ideas** you would like implemented, by all means share them on the [forum](http://forum.asgardcms.com) in the "Comments and Feedback" section.

For **issues/bugs** your having, you can use the Github Issues to post those. All issues are grouped on the [AsgardCms/Platform](https://github.com/AsgardCms/Platform/issues) repository.

If you just want to **talk**, join [our Slack channel](http://slack.asgardcms.com/).
