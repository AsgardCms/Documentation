title: Displaying menus
subtitle: Menu Module
-------

- [Displaying Menus](#displaying-menus)
- [Digging deeper](#digging-deeper)
- [Custom presenter](#custom-presenter)


## <a class="anchor" name="displaying-menus" href="#displaying-menus"></a> Displaying Menus

After creating menus, you can easily display them on your theme using the following notation:

``` .language-php
{!! Menu::get('main') !!}
```
`main` is the name you gave your menu in the administration panel.
That's it. By default this will use boostrap's styling and structure


## <a class="anchor" name="digging-deeper" href="#digging-deeper"></a>  Digging deeper

AsgardCMS leverages a lot of well tested community packages. Managing menus isn't the exception. We use [Pingpong-labs/Menus](https://github.com/pingpong-labs/menus) for handling the menus. You can check out its documentation to learn how to create custom presenters.

The chance will be pretty big you won't be using bootstrap in your clients project. Pingpong-labs/Menus has made this very easy to customise. By creating a custom presenter you can define the structure of your menu.

## <a class="anchor" name="custom-presenter" href="#custom-presenter"></a>  Custom presenter

To create custom presenters you need to create a class that extends the `Pingpong\Menus\Presenters\Presenter` abstract class.
This is an example for Pingpong-labs/Menu's documentation:


``` .language-php

use Pingpong\Menus\Presenters\Presenter;

class ZurbTopBarPresenter extends Presenter
{
    /**
     * {@inheritdoc }
     */
    public function getOpenTagWrapper()
    {
        return  PHP_EOL . '<section class="top-bar-section">' . PHP_EOL;
    }

    /**
     * {@inheritdoc }
     */
    public function getCloseTagWrapper()
    {
        return  PHP_EOL . '</section>' . PHP_EOL;
    }

    /**
     * {@inheritdoc }
     */
    public function getMenuWithoutDropdownWrapper($item)
    {
        return '<li'.$this->getActiveState($item).'><a href="'. $item->getUrl() .'">'.$item->getIcon().' '.$item->title.'</a></li>';
    }

    /**
     * {@inheritdoc }
     */
    public function getActiveState($item)
    {
        return \Request::is($item->getRequest()) ? ' class="active"' : null;
    }

    /**
     * {@inheritdoc }
     */
    public function getDividerWrapper()
    {
        return '<li class="divider"></li>';
    }

    /**
     * {@inheritdoc }
     */
    public function getMenuWithDropDownWrapper($item)
    {
        return '<li class="has-dropdown">
                <a href="#">
                 '.$item->getIcon().' '.$item->title.'
                </a>
                <ul class="dropdown">
                  '.$this->getChildMenuItems($item).'
                </ul>
              </li>' . PHP_EOL;
        ;
    }
}
```

To register this new presenter you need to add it to the package configuration (`config/packages/pingpong/menus/config.php`)

``` .language-php
return array(
    'navbar'        =>  'Pingpong\Menus\Presenters\Bootstrap\NavbarPresenter',
    'navbar-right'  =>  'Pingpong\Menus\Presenters\Bootstrap\NavbarRightPresenter',
    'nav-pills'     =>  'Pingpong\Menus\Presenters\Bootstrap\NavPillsPresenter',
    'nav-tab'       =>  'Pingpong\Menus\Presenters\Bootstrap\NavTabPresenter',

    'zurb-top-bar'  =>  'ZurbTopBarPresenter',
);
```

Next you can call `Menu::render('zurb-top-bar', 'ZurbTopBarPresenter');` before calling the `Menu::get()` method.



