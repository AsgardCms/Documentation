title: Users
subtitle: User Module
-------

- [Getting logged in User](#getting-logged-in-user)
- [Getting logged in User in views](#getting-logged-in-user-in-views)

## <a class="anchor" name="getting-logged-in-user" href="#getting-logged-in-user">Getting logged in User</a>

To get the currently logged in user you can inject the [Authentication interface](https://github.com/AsgardCms/Core/blob/master/Contracts/Authentication.php) in your controller, or a view composer and using the following:

``` .language-php
$user = $this->auth->check();
```

If `$user` is false, means the current user isn't logged in. Otherwise you'll get the currently logged in user.

Check the method signature:

``` .language-php
 /**
* Check if the user is logged in, if so return the current user
* @return bool|object
*/
public function check();
```


## <a class="anchor" name="getting-logged-in-user-in-views" href="#getting-logged-in-user-in-views">Getting logged in User in views</a>

### Recommended: View Composer

The recommended way of attaching the `$currentUser` variable to your desired views is by binding the `CurrentUserViewComposer` to your view(s).

Let's say you want the current user on the `layouts.demo` view, you can add the following code to your module's service provider:

``` .language-php
view()->composer('layouts.demo', \Modules\Core\Composers\CurrentUserViewComposer::class);
```

### Class inheritence

Start by making your public controllers extend the following class:

``` .language-php
Modules\Core\Http\Controllers\BasePublicController
```

Now, in any public view, you have access to a `$currentUser` variable that corresponds to the currently authenticated user. `$currentUser` will evaluate to false if none logged in.
