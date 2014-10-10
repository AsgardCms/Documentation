# Core module : Repositories

The core module has a [base repository](https://github.com/nWidart-Modules/Core/blob/master/Repositories/BaseRepository.php) and an abstract [Eloquent implementation](https://github.com/nWidart-Modules/Core/blob/master/Repositories/Eloquent/EloquentBaseRepository.php).

Your repositories and its interfaces can extend those base class/interfaces for less code duplication.

All you need to do to bind the interface to the implementation 
is something like the following:


``` php
$this->app->bind(
    'Modules\Blog\Repositories\PostRepository',
    function() {
        return new EloquentPostRepository(new Post);
    }
);
```

Instead of passing a string as a second argument to your implementation class, you pass a closure with the implemented class with needs an instance of the model.