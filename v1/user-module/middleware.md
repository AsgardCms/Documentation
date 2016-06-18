title: Middleware
subtitle: User Module
-------

- [Guest middleware](#guest_middleware)
- [Logged in middleware](#logged_in_middleware)

### <a class="anchor" name="guest_middleware" href="#guest_middleware"></a> Guest middleware

The guest middleware makes sure the current route can't be accessed by a logged in user.

By setting a route in the `redirect_route_after_login` config key in the `config/asgard.user.users.php` file, you can make the middleware redirect to your desired route. This defaults to `homepage`.

Example usage: 

``` .language-php
$router->get('login', [
    'middleware' => 'auth.guest', 
    'as' => 'login', 
    'uses' => 'AuthController@getLogin',
]);
```

### <a class="anchor" name="logged_in_middleware" href="#logged_in_middleware"></a> Logged in middleware

The logged in middleware makes sure the current route can **only** be accessed by logged in users. This will redirect the user to the login page if it fails.

Example usage: 

``` .language-php
$router->group(['middleware' => 'logged.in'], function (Router $router) {
    $router->get('account', [
        'as' => 'user.account',
        'uses' => 'Frontend\ProfileController@show',
    ]);
});
```