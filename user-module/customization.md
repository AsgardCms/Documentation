title: Customization
subtitle: User Module
-------

- [Adding data on the users table](#adding-data-on-users-table)
- [Changing login columns](#changing-login-column)
- [Changing redirect route after login](#changing-redirect-route-after-login)


## <a class="anchor" name="adding-data-on-users-table" href="#adding-data-on-users-table"></a> Adding data on the users table

You can add additional columns on the users table if that's really needed. For instance if you want to have an username.

In the users configuration file, located at `config/asgard.user.users.php`, there's a `fillable` key which contains an array of fillable fields for the user object.

Add the fields you want in this array. 


## <a class="anchor" name="changing-login-column" href="#changing-login-column"></a> Changing login columns

On the **Sentinel user driver**, you can choose which columns you would like to use as login attribute. By default this uses the *email* column. In the users configuration file, located at `config/asgard.user.users.php`, you can change these fields in the key `login-columns`.

You'll notice this is an array, indeed Sentinel allows multiple possible login columns.


## <a class="anchor" name="changing-redirect-route-after-login" href="#changing-redirect-route-after-login"></a> Changing redirect route after login

In the users configuration file, located at `config/asgard.user.users.php`, there is key called `redirect_route_after_login`. This is the route used to redirect to after a successful login. 

This defaults to the `homepage` route.
