title: Managing menus
subtitle: Menu Module
-------

## <a class="anchor" name="menus-explained" href="#menus-explained"></a> Menus explained

Menus in AsgardCMS are used like in any other site, to have a series of links available somewhere on your fornt-end layout. You can have as menu menus as you want, a top-menu, a main menu, footer menu and so on. 
I
Each menu can have multiple **menuitems**. A menuitem can be linked to a page, a module or a completely external UR**L** (link to facebook/twitter/... for instance).


One thing to note, is that you need to have one menu marked as **primary menu**. This primary menu will be used for your front-end routes.

Let say you have a primary menu called '*Main*', all the menu items inside it, will be accessible publically by the URI you add to it. 

So if you want the blog module to be available at `yousite.com/bloggy` you only have to add a menu item in the primary menu, with the UR**I** set to `bloggy`, and linked to the blog module. From now on you'll be able to access your blog like expected. When viewing a blog post, they will be available at `yoursite.com/bloggy/post-slug`.

This is ofcourse all default behaviour that can be customised as needed on a per project basis.

