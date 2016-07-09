title: Widgets
subtitle: Dashboard Module
-------

- [Defining widgets](#defining-widgets)

The dashboard is a very important part of the back-end of the CMS. It's the first thing your client will see when he logs into the backend. In asgard, your modules can define a set of widgets that will be displayed on the dashboard. These widgets can be simple counts, tables, or pretty much whatever you want.

Widgets location are saved on a per user basis. Each logged in user with the correct permissions can re-arrange the widgets however he or she prefers.

## <a name="defining-widgets" class="anchor" href="#defining-widgets">Defining widgets</a>

Creating widgets is very easy and straightforward. A widget is composed of the following parts:

- A widget class
- A widget view

### Widget class

First you'll have to create a widget class that extends an abstract class: `BaseWidget`. This BaseWidget class will enforce you to implement the following methods:

- name (*string*): The name of the module. This needs to be on word. You can either choose to use camelCase, snake_case, or whatever you prefer as long as this is **one word**.
- options (*array*): This is an array of options that your widget can have.

	Possible options are:
	
	- x
	- y
	- width
	- height
	
- view (*string*): Define which view needs to be used for you widget
- data (*array*): Choose what data to send to your view. The array keys will be available in the view, just like a regular `view::make`.

[View an example widget class.](https://github.com/AsgardCms/Blog/blob/master/Widgets/PostsWidget.php)

### Widget view

Now you can make your widget view. You can find some inspiration on the widgets page of the [Admin LTE theme](https://almsaeedstudio.com/themes/AdminLTE/pages/widgets.html).


### Registering the widget

As a final step you need to define your active widgets. To do so, you need to add a `Widgets` array in your `module.json` file, with an array of widget classes.

For instance, the Blog module has:

``` .language-javascript
"widgets": [
    "Modules\\Blog\\Widgets\\PostsWidget",
    "Modules\\Blog\\Widgets\\CategoriesWidget",
    "Modules\\Blog\\Widgets\\LatestPostsWidget"
],
```

Your widget will now be displayed on the dashboard.

