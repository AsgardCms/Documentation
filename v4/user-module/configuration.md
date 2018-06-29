title: Configuration
subtitle: User Module
-------

- [Adding data on the users table](#adding-data-on-users-table)
- [Changing login columns](#changing-login-column)
- [Changing redirect route after login](#changing-redirect-route-after-login)
- [Changing redirect route if not logged in](#changing-redirect-route-not-logged-in)
- [Allow/Disallow user registrations](#user-registrations)
- [User driver](#user-driver)

The **User module** configuration file can be found at `config/asgard/user/config.php`.

## <a class="anchor" name="adding-data-on-users-table" href="#adding-data-on-users-table">Adding data on the users table</a>

You can add additional columns on the users table if that's really needed. For instance if you want to have an username.

This defaults to the following fields:

``` .language-php
'fillable' => [
    'email',
    'password',
    'permissions',
    'first_name',
    'last_name',
],
```

## <a class="anchor" name="changing-login-column" href="#changing-login-column">Changing login columns</a>

On the **Sentinel user driver**, you can choose which columns you would like to use as login attribute. By default this uses the *email* column.

``` .language-php
'login-columns' => ['email'],
```

You'll notice this is an array, indeed Sentinel allows multiple possible login columns.


## <a class="anchor" name="changing-redirect-route-after-login" href="#changing-redirect-route-after-login">Changing redirect route after login</a>

Define which route to redirect to after a successful login.

This defaults to the `homepage` route.

``` .language-php
'redirect_route_after_login' => 'homepage',
```

## <a class="anchor" name="changing-redirect-route-not-logged-in" href="#changing-redirect-route-not-logged-in">Changing redirect route if not logged in</a>

Define which route the user should be redirected to after accessing a resource that requires to be logged in.

``` .language-php
'redirect_route_not_logged_in' => 'auth/login',
```

## <a class="anchor" name="user-registrations" href="#user-registrations">Allow/Disallow user registrations</a>

Allow anonymous user registration. If this is diabled the link to register a new account and its routes will be disabled.

``` .language-php
'allow_user_registration' => true,
```


## <a class="anchor" name="user-driver" href="#user-driver">User driver</a>

Define which user driver to use.

It defaults to **Sentinel**.

``` .language-php
'driver' => 'Sentinel',
```

Make sure to install the wanted driver on composer first.

Also, be sure to check out the [User Drivers](https://asgardcms.com/en/docs/user-module/drivers) documentation page for additional info on how to create new user & role drivers.

