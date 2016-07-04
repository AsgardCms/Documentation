title: Contributing
subtitle: Getting Started
-------

- [Getting setup](#getting-setup)
- [Style guide](#style-guide)
- [Making changes](#making-changes)
- [Adding or updating translations](#adding-updating-translations)
- [Additional resources](#additional-resources)

### <a name="getting-setup" class="anchor" href="#getting-setup"></a> Getting setup

### Modules 

- Have an installation of [AsgardCMS/Platform](https://github.com/AsgardCms/Platform) 
- Remove the `.git/` directory
- Remove all modules from `composer.json` file (or only the one you want to contribute to)
- `cd` into the `Modules/` folder and clone each Module individually (or only the one you want to contribute to)
- Install AsgardCMS as usual `php artisan asgard:install`

### Themes

This is the same as modules except `cd`-ing into the `Themes/` folder and cloning desired themes in there.

### <a name="style-guide" class="anchor" href="#style-guide"></a> Style guide

Please note AsgardCMS follows **[PSR-1](http://www.php-fig.org/psr/psr-1/)** and **[PSR-2](http://www.php-fig.org/psr/psr-2/)**. Please make sure your code follows those standards.

You can use a great tool : **[PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)** to make sure everything is following the correct coding style.

Every module has a `.php_cs` config file to run **php-cs-fixer** with:

``` .language-bash
$ cd Modules/{ModuleName}
$ php-cs-fixer fix . --config-file=".php_cs" --verbose
```

To avoid having to type this every time, I have this command aliased to `pcf`, like so:

``` .language-bash
pcf="php-cs-fixer fix . --config-file='.php_cs' --verbose"
```
Now I can type `pcf` in the root directory of the module, and it'll just work, giving that there's a `.php_cs` file.


### <a name="making-changes" class="anchor" href="#making-changes"></a> Making changes

Once you have your copy of AsgardCMS installed and configured for contributing purposes, you're ready to make changes.

AsgardCMS follows a workflow similar to **[Git Flow branching model](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow/)**.

This means:

- For a new feature: 
	- On `master` branch,
	- Create a branch `feature/your-new-feature-name`,
	- Add you changes,
	- Make sure the test suite for the module still passes,
	- [Squash commits](https://ariejan.net/2011/07/05/git-squash-your-latests-commits-into-one/) if necessary to create a nice history,
	- Send a pull request to the `master` branch of the module/theme your modifying.
- For a hotfix:
	- On `master` branch,
	- Create a branch `hotfix/your-hotfix-name`,
	- Add a failing test that reproduces the found bug,
	- Add you changes by making the test pass,
	- [Squash commits](https://ariejan.net/2011/07/05/git-squash-your-latests-commits-into-one/) if necessary to create 	a nice history,
	- Send a pull request to the `master` branch of the module/theme your modifying.

### <a name="adding-updating-translations" class="anchor" href="#adding-updating-translations"></a> Adding or updating translations

Adding new translations or updating existing translations to core modules is very easy in AsgardCms. All translations are centralised in the [Translation](https://github.com/AsgardCms/Translation) module. 

All you need to do is fork that module, and add and/or update existing translations. 

The translations are located in the `Resources/lang` folder, each module has its own subfolder, with under that the different locales.

If you want to add a new language, duplicate the `en` folder of each module and renaming it to your desired locale. The English translations will usually the more complete ones, that's why it's best to use those as a starting point. 


### <a name="additional-resources" class="anchor" href="#additional-resources"></a> Additional resources

* [General GitHub documentation](http://help.github.com/)
* [GitHub pull request documentation](http://help.github.com/send-pull-requests/)
* Join the [AsgardCms Slack](http://slack.asgardcms.com/) channel to chat

