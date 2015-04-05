# MVC Base Plugin for Wordpress based on CakePHP

This plugin helps you to create a MVC (VC only for now) structure in your
plugins. But that's not all, here is a list of some features:

- MVC architecture in your plugins (maintainability)
- A pretty good and easy plugin skeleton
- Real namespacing for your plugins
- Avoid to create function names as aVeryCoolPlugin_activate and stop worrying
	of create unique function names
- Automatic slugs for your menu items (using the `defaultMenus` attribute)
- Automatic submenu items (using the `defaultMenus` attribute)
- Automatic AJAX handler mapping to your controllers methods
- An easier way to add css, images and scripts
- A better way to return content by using Views instead of functions echoing
- Just drop it in your wordpress and start extending your plugins

So, if you are familar with CakePHP framework and you need/want to start
writing some wordpress plugins, the it's your package. If you are not familiar
with CakePHP you don't have to worry because the MVC architecture is very easy
to understand and use. I wrote it not as a plugin, because if you write 3
plugins based on it you will need to duplicate some files. So, it becomes
reusable.

## How to use it:

Easy, just drop this package in your `wp-includes` folder (doesn't have to be
right there, but it's a recommended location). Then create your plugin's
initial folder in `wp-content/plugins/your-plugin` and file `your-plugin.php`.

In your plugin's main file `your-plugin.php` the first line must be the
namespace declaration, the recommended statement to prevent user from accesing
your files directly and your plugin's doc block/license (**_I will ommit it_**)

```
<?php
# file: your-plugin.php
namespace YourPlugin;

defined("ABSPATH") or die( "-1" );

?>
```

Then, require the MVC Plugin file and declare the use of its namespaces and
classes.

```
<?php
# file: your-plugin.php
namespace YourPlugin;

defined("ABSPATH") or die( "-1" );
defined("DS") or define("DS", DIRECTORY_SEPARATOR);

require_once ABSPATH . WPINC . DS . "wp-mvc" . DS . "Plugin.php.inc";
use MVC\Plugin;
use MVC\PluginInterface;

?>
```

Finally create your plugins class extending from our plugin base and
interface, and initialize it. As you will see, the `PluginInterface` force us
to declare some methods:

```
<?php
# file: your-plugin.php
namespace YourPlugin;

defined("ABSPATH") or die( "-1" );

require_once ABSPATH . WPINC . DS . "wp-mvc" . DS . "Plugin.php.inc";

use MVC\Plugin;
use MVC\PluginInterface;

class YourPlugin extends Plugin implements PluginInterface{

	public static function activate(){}
	public static function deactivate(){}
	public static function uninstall(){}

}

YourPlugin::init();

?>
```
## Folder structure

The folder structure required in your plugin is:

- your-plugin
	- assets (_also known as webroot_)
		- css
		- js
		- img
	- controllers
	- views
	- your-plugin.php file

You can create a symlink named `webroot` if you feel the need to keep the
CakePHP's folder structure (on windows use the cmd and type `mklink /D assets webroot`)

Following Cake's naming convention, a controller for users will be stored in
your controllers folder as `UsersController.php`. And the views for its
methods will be stored in your views folder with the same name as your
methods, for example `index.tpl` (I'm using tpl file extension instead of
ctp).

Your controllers must follow these rules:

- Declare your plugin's namespace
- Declare the use of our plugin's base controller class
- Your controller class must extend from our controller

```
<?php
# file: controllers/UsersController.php
# Declare your Plugin's namepace
	namespace YourPlugin\Controller;

# Declare the use of the MVC Controller class
	use MVC\Controller;

# Your controller
	class UsersController extends Controller{

		public function index(){}

	}
?>
```

I wrote this mini MVC this weekend, so there are a lot of more things to
include such as Models. I will include an example plugin using this MVC.
