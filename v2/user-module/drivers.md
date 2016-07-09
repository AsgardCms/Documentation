title: Drivers
subtitle: User Module
-------

- [User and Role providers](#user-and-role-providers)
- [Implementing custom providers](#implementing-custom-providers)


The user module brings three important interfaces:

- `Authentication` ([view interface](https://github.com/AsgardCms/User/blob/2.0/Contracts/Authentication.php))
- `UserRepository` ([view interface](https://github.com/AsgardCms/User/blob/2.0/Repositories/UserRepository.php))
- `RoleRepository` ([view interface](https://github.com/AsgardCms/User/blob/2.0/Repositories/RoleRepository.php))

Thanks to these interface, the user and role systems can be completely decoupled from the implementation. This is what enables AsgardCMS to give you the option to either use Sentry or Sentinel out of the box.

## <a class="anchor" name="user-and-role-providers" href="#user-and-role-providers">User and Role providers</a>

AsgardCMS comes **out of the box** with the following User and Role providers:
  
- [Cartalyst Sentinel](https://cartalyst.com/manual/sentinel/1.0?utm_source=asgard-cms&utm_medium=readme&utm_campaign=asgard-cms)

## <a class="anchor" name="implementing-custom-providers" href="#implementing-custom-providers">Implementing custom providers</a>

You are absolutely free to implement other user/role/authentication providers. You could for instance make an implementation for the popular packages Confide and Entrust, or maybe you're satisfied with the basic laravel implementation. 

To make a new implementation its very easy, you simply need to implement the said interfaces and place the implementation in the `Repositories/` folder.

For your inspiration you can check how Sentry and Sentinel are implemented:

- [Sentinel](https://github.com/AsgardCms/User/tree/master/Repositories/Sentinel)

Once implemented, don't forget to change the `UserServiceProvider` class to bind the interfaces to your implementation. You can do this in the [registerBindings()](https://github.com/AsgardCms/User/blob/master/Providers/UserServiceProvider.php#L75) method.

For the spirit of open source, if you have successfully implemented another driver, consider sending a pull-request to the User Module repository so others can benefit from your hard work too.

