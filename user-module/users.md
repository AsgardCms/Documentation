title: Users
subtitle: User Module
-------

- [Getting logged in User](#getting-logged-in-user)

## <a class="anchor" name="getting-logged-in-user" href="#getting-logged-in-user"></a> Getting logged in User

To get the currently logged in user you can inject the [Authentication interface](https://github.com/AsgardCms/Core/blob/develop/Contracts/Authentication.php) and checking like so:

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

