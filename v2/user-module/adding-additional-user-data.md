title: Adding additional user data
subtitle: User Module
-------

- [Creating a Profile module](#creating-a-profile-module)
- [Adding custom profile fields](#adding-custom-profile-fields)
- [Publishing user views](#publishing-user-views)
- [Adding custom fields on the register view](#adding-custom-fields-on-register-view)
- [Setting up relations](#setting-up-relations)
- [Adding data on the users table](#adding-data-on-users-table)


The User module is nice for handling authentication and registration, but it is very likely that you are going to want to add more data to your user then the default first and last name. Here we're going to see how to add more data to our user.


## <a class="anchor" name="creating-a-profile-module" href="#creating-a-profile-module"></a> Creating a Profile module

First thing we need to do is creating a Profile module. You can do this using the [Module Scaffold](https://asgardcms.com/en/docs/workshop-module/module-scaffold) tool, or by creating the module manually.

For this purpose of this guide, we'll be using the module scaffold command. Start by running `php artisan asgard:module:scaffold` in your terminal, enter `your-vendor-name/profile` as the module name. Next select Eloquent, followed by entering the `Profile` entity. Finally leave the rest empty to finalise the scaffolding. 

Don't forget to add the module in the `Modules/.gitignore` file by adding `!Profile` in that file.

By default the scaffolder tool will create entities as if they were translatable, we don't need this feature on the Profile so we can remove the `ProfileTranslation` entity and the migrations for the translations.


## <a class="anchor" name="adding-custom-profile-fields" href="#adding-custom-profile-fields"></a> Adding custom profile fields

Open the migration file that was generated, and add the fields you would like to have on the use profile. As an example:

``` .language-php
Schema::create('profile__profiles', function (Blueprint $table) {
    $table->increments('id');
    $table->integer('user_id')->unsigned();
    $table->string('tel')->nullable();
    $table->string('street')->nullable();
    $table->string('number')->nullable();
    $table->string('additional')->nullable();
    $table->string('zip')->nullable();
    $table->string('place')->nullable();

    $table->timestamps();
    $table->foreign('user_id')->references('id')->on('users')->onDelete('cascade');
});
```

Now run the migrations using `php artisan module:migrate Profile`.


## <a class="anchor" name="publishing-user-views" href="#publishing-user-views"></a> Publishing user views

Next, we're going to add those fields on on register page. Since the register views are in the User module, which we cannot edit (**consider any module not in the .gitignore as a package in the vendor folder**). To customize the login and register views we're going to publish those views using the following command:

``` .language-php
php artisan vendor:publish --provider="Modules\User\Providers\UserServiceProvider"
```

After this you'll see the views have been published in the `resources/views/asgard` folder.


## <a class="anchor" name="adding-custom-fields-on-register-view" href="#adding-custom-fields-on-register-view"></a> Adding custom fields on the register view


Now that we have the register view, open it and add the fields by following the following field naming convention :

``` .language-php
profile[your-field-name]
```

An example from our migration :

``` .language-php
<div class="form-group{{ $errors->has('profile.tel') ? ' has-error has-feedback' : '' }}">
    {!! Form::label('profile[tel]', trans('profile::profiles.tel')) !!}
    <input class="form-control" placeholder="{{ trans('profile::profiles.tel') }}"
           name="profile[tel]" type="text" id="profile[tel]" value="{{ Input::old('profile.tel') }}">
    {!! $errors->first('profile.tel', '<span class="help-block">:message</span>') !!}
</div>

<div class="form-group{{ $errors->has('profile.street') ? ' has-error has-feedback' : '' }}">
    {!! Form::label('profile[street]', trans('profile::profiles.street')) !!}
    <input class="form-control" placeholder="{{ trans('profile::profiles.street') }}"
           name="profile[street]" type="text" id="profile[street]" value="{{ Input::old('profile.street') }}">
    {!! $errors->first('profile.street', '<span class="help-block">:message</span>') !!}
</div>

<div class="form-group{{ $errors->has('profile.number') ? ' has-error has-feedback' : '' }}">
    {!! Form::label('profile[number]', trans('profile::profiles.number')) !!}
    <input class="form-control" placeholder="{{ trans('profile::profiles.number') }}"
           name="profile[number]" type="text" id="profile[number]" value="{{ Input::old('profile.number') }}">
    {!! $errors->first('profile.number', '<span class="help-block">:message</span>') !!}
</div>

 <div class="form-group{{ $errors->has('profile.additional') ? ' has-error has-feedback' : '' }}">
    {!! Form::label('profile[additional]', trans('profile::profiles.additional')) !!}
    <input class="form-control" placeholder="{{ trans('profile::profiles.additional') }}"
           name="profile[additional]" type="text" id="profile[additional]" value="{{ Input::old('profile.additional') }}">
    {!! $errors->first('profile.additional', '<span class="help-block">:message</span>') !!}
</div>

<div class="form-group{{ $errors->has('profile.zip') ? ' has-error has-feedback' : '' }}">
    {!! Form::label('profile[zip]', trans('profile::profiles.zip')) !!}
    <input class="form-control" placeholder="{{ trans('profile::profiles.zip') }}"
           name="profile[zip]" type="text" id="profile[zip]" value="{{ Input::old('profile.zip') }}">
    {!! $errors->first('profile.zip', '<span class="help-block">:message</span>') !!}
</div>

<div class="form-group{{ $errors->has('profile.place') ? ' has-error has-feedback' : '' }}">
    {!! Form::label('profile[place]', trans('profile::profiles.place')) !!}
    <input class="form-control" placeholder="{{ trans('profile::profiles.place') }}"
           name="profile[place]" type="text" id="profile[place]" value="{{ Input::old('profile.place') }}">
    {!! $errors->first('profile.place', '<span class="help-block">:message</span>') !!}
</div>
```

And that's all there is to it to add our custom fields on the view.

## <a class="anchor" name="setting-up-relations" href="#setting-up-relations"></a> Setting up relations

The final thing we need to do is setting up the relation, both on the Profile entity as on the User entity. A profile belongs to a user and a user belongs to a profile.

### On Profile entity

This one is easy, though we need to take into account AsgardCms can have multiple user drivers, so our `user()` method on the Profile will look like this:


``` .language-php
public function user()
{
    $driver = config('asgard.user.users.driver');

    return $this->belongsTo("Modules\\User\\Entities\\{$driver}\\User");
}
```
This is added on the Profile entity found at `Modules/Profile/Entities/Profile.php`. 

We're reading the user driver from the configuration and using that to setup our relation.

Now to get the user from a profile just use `$profile->user->id`.

### On User entity

This one is special since we cannot edit our User module directly, since this module is managed by composer and is not present in our `Modules/.gitignore` file.

To add the relation on our User, we need to create a `relations.php` file in the `Config` folder of our application. 

This is what this file looks like for user User relation:

``` .language-php
<?php

return [
    'User' => [
        'profile' => function ($self) {
            return $self->belongsTo('Modules\Profile\Entities\Profile', 'id', 'user_id')->first();
        }
    ]
];
```

We can now access the user profile information using `$user->profile->street`.

## <a class="anchor" name="adding-data-on-users-table" href="#adding-data-on-users-table"></a> Adding data on the users table

You can add additional columns on the users table if that's really needed. For instance if you want to have an username.

In the users configuration file, located at `config/asgard.user.users.php`, there's a `fillable` key which contains an array of fillable fields for the user object.

Add the fields you want in this array. 
