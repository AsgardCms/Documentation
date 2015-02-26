title: Module Scaffold
subtitle: Workshop Module
-------

- [Introduction](#introduction)
- [Usage](#usage)


### <a class="anchor" name="introduction" href="#introduction"></a> Introduction

The module scaffolder is a command line tool that will give you the ability to generate modules in a matter of seconds.

To have a quick idea on what it doesn you can check ou [this quickcast](http://quick.as/loki7l0).

### <a class="anchor" name="usage" href="#usage"></a> Usage

The usage is pretty simple and straightforward. Simply call the following command from the project root:

``` .language-bash
php artisan asgard:module:scaffold
```

You will be asked the following questions:


- What is the module name ?
	
	This is in the following format `vendor/name` all lowercase.
- Do you wish to use Doctrine or Eloquent ?

	This is to know what kind of Entities to generate.

- Enter your desired entites

	You can enter as many as you like, when you're done leave empty and the next question will come up.
	
- Enter you desired value objects
	
	Again, you can enter as many as you like, when you're done leave empty.
	

When these questions are answered your module will be generated. You will still need to add the properties to the eloquent migration and/or to the entity (if using Doctrine).

Before seeing the newly created module on the admin dashboard you will have to give you access to the new module. Go the the **User > Roles** view and edit the Admin role to give you permission to the new module.

