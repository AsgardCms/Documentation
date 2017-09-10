title: Repositories
subtitle: Core Module
-------

- [Usage](#usage)
- [Non translatable usage](#non_translatable_usage)




## <a class="anchor" name="usage" href="#usage">Usage</a>


The core module has a [base repository](https://github.com/nWidart-Modules/Core/blob/master/Repositories/BaseRepository.php) and an abstract [Eloquent implementation](https://github.com/nWidart-Modules/Core/blob/master/Repositories/Eloquent/EloquentBaseRepository.php).

Your repositories and its interfaces can extend those base class/interfaces for less code duplication.

All you need to do to bind the interface to the implementation 
is something like the following:


``` .language-php
$this->app->bind(PostRepository::class, function() {
    return new EloquentPostRepository(new Post);
});
```

Instead of passing a string as a second argument to your implementation class, you pass a closure with the implemented class with needs an instance of the model.


## <a class="anchor" name="non_translatable_usage" href="#non_translatable_usage">Non translatable usage</a>


If your entity isn't translatable you'll have to overwrite the `all` and `find($id)` methods on your eloquent repository implementation:

``` .language-php
public function find($id)
{
    return $this->model->find($id);
}

public function all()
{
    return $this->model->orderBy('created_at', 'DESC')->get();
}
```