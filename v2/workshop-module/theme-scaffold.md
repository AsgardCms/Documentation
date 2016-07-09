title: Create a theme
subtitle: Workshop Module
-------

- [Introduction](#introduction)
- [Usage](#usage)
- [Manual creation](#manual-creation)


## <a class="anchor" name="introduction" href="#introduction">Introduction</a>

The theme scaffolder is a command line tool that will give you the ability to generate themes in a matter of seconds.

To have a quick idea on what it does you can check out [this quickcast](http://quick.as/epduvv4b).

## <a class="anchor" name="usage" href="#usage">Usage</a>

The usage is pretty simple and straightforward. Simply call the following command from the project root:

``` .language-bash
php artisan asgard:theme:scaffold
```

You will be asked the following questions:

- What is the theme name
	
	This is in the following format `vendor/name` all lowercase.
- Do you wish to make a backend or front end theme ?

And that's it. You'll find you newly created theme under the `Themes/` directory.


## <a class="anchor" name="manual-creation" href="#manual-creation">Manual creation</a>

You can create themes manually as well, all a theme needs is the `theme.json` file to be registerable on the [Stylist package](https://github.com/floatingpointsoftware/stylist).

After you created the `theme.json` file, run a `php artisan cache:clear`.

> In both cases you will need to active the theme from the backend Settings page, "Front end template".