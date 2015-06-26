title: Theme Scaffold
subtitle: Workshop Module
-------

- [Introduction](#introduction)
- [Usage](#usage)


### <a class="anchor" name="introduction" href="#introduction"></a> Introduction

The theme scaffolder is a command line tool that will give you the ability to generate themes in a matter of seconds.

To have a quick idea on what it does you can check out [this quickcast](http://quick.as/epduvv4b).

### <a class="anchor" name="usage" href="#usage"></a> Usage

The usage is pretty simple and straightforward. Simply call the following command from the project root:

``` .language-bash
php artisan asgard:theme:scaffold
```

You will be asked the following questions:

- What is the theme name
	
	This is in the following format `vendor/name` all lowercase.
- Do you wish to make a backend or front end theme ?

And that's it. You'll find you newly created theme under the `Themes/` directory.
	 