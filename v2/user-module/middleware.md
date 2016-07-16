title: Middleware
subtitle: User Module
-------

- [Guest middleware](#guest_middleware)
- [Logged in middleware](#logged_in_middleware)
- [AuthorisedApiToken](#authorised-api-token)
- [AuthorisedApiTokenAdmin](#authorised-api-token-admin)

## <a class="anchor" name="guest_middleware" href="#guest_middleware">Guest middleware</a>

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

## <a class="anchor" name="logged_in_middleware" href="#logged_in_middleware">Logged in middleware</a>

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


## <a class="anchor" name="authorised-api-token" href="#authorised-api-token">AuthorisedApiToken</a>

This middleware allows you to protect your API routes with a user API key system.

When protected your api routes with this middleware, and failing to provide an API key during the request, a `403 forbidden` response will be sent.

``` .language-php
$router->group(['prefix' => 'v1', 'middleware' => 'api.token'], function (Router $router) {
	// Routes proteted by the middleware
});
```

## <a class="anchor" name="authorised-api-token-admin" href="#authorised-api-token-admin">AuthorisedApiTokenAdmin</a>

This is similar to the `AuthorisedApiToken` middleware, with one addition that it checks if the given API token belongs to an administrator. This can be usuful if you have api routes that must only be accessed by an administrator.

Since AsgardCMS 2.0, all default API routes from the backend are protected by this middleware. 

``` .language-php
$router->group(['prefix' => 'v1', 'middleware' => 'api.token.admin'], function (Router $router) {
	// Routes proteted by the middleware
});
```