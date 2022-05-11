# Build 1.2.0 (WIP)

## UX/UI Improvements
- Added support for autocompletion for all Winter provided CLI commands.
- Added `complete()` function to the `create:command` Command scaffolding for providing autocompletion in console commands. (run `artisan completion --help` to setup autocompletion in your terminal)
- Added autocompletion support to the following commands:
    - `plugin:disable $name`
    - `plugin:enable $name`
    - `plugin:refresh $name`
    - `plugin:rollback $name $rollbackVersion`
    - `winter:passwd $username` (last 20 updated backend users)
- Changed recommended language mode for component partial files to `wintercms-twig` instead of `twig`.
- The `.env` file is now a first class citizen in Winter and configuration files refer to it by default. You can continue to run `winter:env` to generate a file pulling from your configuration to provide the default values.
- The default configuration for the testing environment now includes an override to store files generated / modified throughout the test suite in a folder under tests/storage instead of polluting your regular local storage folder with files from tests that failed to clean up after themselves well enough.
- Added `migrate` as an alias to `winter:up` to simplify transitioning to Winter from Laravel
- Improved confirmation logic for potentially destructive console commands.
- Added ability for the `mix:watch` command to clean up after itself when terminated with SIGTERM.
- Made it easier to track down issues with the `ImageResizer` class by only removing the resizer configuration from the Cache after the resizer has been successfully instantiated.
- Backend template files (layouts, views, & partials) now use the `.php` extension which reduces confusion about what templating language is used for backend template files. `.htm` files are still supported, but not recommended.
- Icon library updated from Font Awesome version 4 to 6, bringing over 1,300 new icons.

## API Changes
- `server.php` is no longer needed in order for `artisan serve` to function; it can be removed.
- An application key is no longer provided by default, if your Winter instance is missing one just run `artisan key:generate` and one will be generated and set for you.
- Added `@snowboard.base`, `@snowboard.request`, `@snowboard.attr`, `@snowboard.extras`, & `@snowboard.extras.css` AssetCombiner aliases.
- Module route registration should no longer require being wrapped in `App::before()` to support plugin's overriding them
- The following Twig environments are now registered by the application and can be resolved by calling `App::make($environmentName);`:
    - `twig.environment` The default System TwigEnvironment, is used by the `Twig::parse()` parser
    - `twig.environment.mailer` The Mailer TwigEnvironment, used by the `MailManager` class when rendering emails
    - `twig.environment.cms` The CMS TwigEnvironment, used by the CMS when rendering CMS templates
- Added the `System\Classes\MarkupManager::makeBaseTwigEnvironment(TwigLoader $loader, array $options)` static helper method that returns the basic `TwigEnvironment` that should be used by any custom Twig implementation in Winter CMS (i.e. applies the default security policy and `SystemTwigExtension`).
- Removed the `transaction()`, `beginTransaction()`, and `endTransaction()` methods from `System\Classes\MarkupManager` since "markup transactions" was a hacky workaround originally implemented due to global polution of the single Twig environment. This is no longer required with the use of multiple, separate twig environments.
- Added support for the `{% spaceless %}` and `{% filter %}` Twig tokens to the core as Twig v3 removed them; it is recommended to avoid using them however.
- The SchemaBuilder is now bound to `db.schema` instead of only resolved directly through the `Schema` facade.
- Laravel's migration commands have been removed / aliased to the relevant Winter commands as they did not function with Winter and never have.
- Facades must return string keys rather than objects (See https://github.com/laravel/framework/pull/38017)
- `Winter\Storm\Support\Facades\Str` facade has been removed, use `Winter\Storm\Support\Str` directly instead.
- The base `ModuleServiceProvider` no longer needs a call to `parent::register($module)` in the `register()` method as route registration is now handled in the `boot()` method.
- Added two new events (`system.beforeRoute` and `system.route`) that fire before and after the system route registration respectively and moved the registration of the Backend and CMS module routes to be after the system route registration. The CMS module's routes should now always be the last routes registered regardless of what happens.
- The `ThemeInstall`, `ThemeRemove`, `ThemeList`, `ThemeUse`, & `ThemeSync` console commands have been moved from the System module to the CMS module.
- Removed the `getAdapter()` method from Storage disk instances
- Added `getPathPrefix()` and `setPathPrefix()` methods to Storage disk instances
- Fixed issue where running `winter:version --changes` would always display "We have detected the following modifications:" even when no modifications were detected.
- The signature for `$twig->loadTemplate()` has been changed, use `$twig->load()` instead.
- Added support for [anonymous migrations](https://laravel-news.com/laravel-anonymous-migrations) and made them the default when creating new migrations with `artisan create:model`.
- Moved all scaffolding commands out of `Winter\Storm` and into their relevant Modules (`Backend`, `CMS`, & `System`).
- Added `Winter\Storm\Console\Command` base class that adds helpers for making it easier for commands to implement suggested values for autocompletion.
- Added `$nameFrom` property and `getNameInput()` method to the `Winter\Storm\Scaffold\GeneratorCommand` to enable checking for reserved names when generating code via scaffolding commands. Also made some method signature type hint changes to the class, be sure to review and apply them accordingly in any custom uses of that base class.
- Removed `getPluginIdentifier()` method from the `Winter\Storm\Scaffold\GeneratorCommand` class and added a new base class for scaffolding resources that are specific to plugins: `System\Console\BaseScaffoldCommand`.
- Added support for autocompletion of the `plugin` argument for scaffolders that extend `System\Console\BaseScaffoldCommand`.
- Added support for generating localization messages by calling a `getLangKeys()` method defined on the scaffolding command during the execution process. This method can use the `$this->vars` property and `$this->laravel->getLocale()` method to return an associative array of message keys without the author prefix and their values for the current locale.
- Added several helpers in the scaffolding template files:
    - `plugin_id` -> lowercase version of a plugin's identifier
    - `plugin_code` -> Studly case version of the plugin's identifier
    - `plugin_url` -> `author/plugin`, used in `Backend::url()` calls
    - `plugin_folder` -> `author/plugin`, used when generating paths to files with the `$` plugins directory path symbol or the `~` application path symbol.
    - `plugin_namespace` -> Studly case version of the plugin's identifier in namespace form (i.e. `Author\Plugin`)
- Added `alert()` helper to the Winter `Command` base class that improves on the Laravel default by adding support for wrapping long alert messages to multiple lines.
- Added `Winter\Storm\Console\Traits\ConfirmsWithInput` trait provides the `confirmWithInput($message, $requiredInput)` method to require the user to input the required input string in order before proceeding with running the command.
- Version number reported by `artisan --version` will now include `Winter CMS`.
- Changed `System\Classes\VersionManager->getDatabaseHistory($pluginCode)` from protected to public.
- Added `System\Console\Traits\HasPluginInput` trait that provides helpers for when a console command interacts with plugin names as input arguments.
- Removed `varcharmax` as a configuration option for `mysql` database connections.
- Made the `getStorageDisk()` and `getMediaPath()` methods on `System\Classes\MediaLibrary` public instead of protected.
- Added `add{$RelationType}Relation($name, $config)` methods to the `HasRelationships` trait that make it easier to dynamically add new relationships to existing model classes.
- Added `Winter\Storm\Parse\EnvFile` parsing class for handling modifying the contents of environment (`.env`) files through PHP.
- Added `Winter\Storm\Parse\PHP\ArrayFile` parsing class for handling modifying the contents of Array Files (PHP config & localization files that return a single array and are used for storing data). The `Winter\Storm\Config\ConfigWriter` class has been rewritten to use the `ArrayFile` parser internally.
- Added support for `multiple: bool` property on `type: fileupload` fields in the Theme Customization section to choose between an `attachOne` and `attachMany` relationship.
- Changed how YAML processors (added in v1.1.3) work; preprocessors are now only engaged if parsing the provided contents throws an exception.
- The `backend.layout.extendHead` event now passes `auth` or `default` as the value for `layout` instead of `auth.htm` or `default.htm`.
- `Symfony\Component\Debug\Exception\FatalErrorException` has been removed, use `Symfony\Component\ErrorHandler\Error\FatalError` instead.

## Bug Fixes
- `route:list` and `route:cache` now support module routes out of the box.
- Replaced usage of `{% filter %}` in the demo theme with `{% apply %}` instead.
- Fixed issue where the default CMS twig environment was unable to be extended or reused, resolve `twig.environment.cms` before it's used by the CMS in order to use or modify it.
- Fixed issue where calling `Twig::parse()` before doing anything that rendered Mail content (i.e. sending an email) would cause the Mail twig rendering to stop working.
- Fixed inconsistency where `CmsCompoundObject` instances were not using the default CMS twig environment.
- Removed requirement for a `Cms\Classes\Controller` instance on the `Cms\Twig\DebugExtension` making it easier to reuse elsewhere.
- `winter:version` will now only normalize file contents before hashing if the file is a valid text-based file which improves the reliability of change detection on Windows.
- `winter:passwd` now returns the status codes instead of using `exit($code)`
- Fixed support for morphOne/hasOne relations in FormModelSaver
- Fixed issue where paths returned by the UploadableWidget could have two leading directory separators.
- Fixed issue where attempting to interact with a Model instance before the DatabaseServerProvider boot() method was called would prevent any "nice" model events from actually working.
- Fixed issue where the `key:generate` command wouldn't set the `APP_KEY` value in the `.env` file if the `.env` file didn't exist yet.
- Fixed issue where the `Cms\Classes\Page` `isActive` property wasn't being set if the URL was set to `/` and the currently requested URL was the home page.
- Fixed issue where if the underlying data behind a datasource changes through manual intervention (either in the database or the filesystem) before running `theme:sync` it wasn't being detected by the `theme:sync` command.

## Security Improvements
- Winter instances no longer come with a default application key set, `artisan key:generate` should be used to generate one.

## Translation Improvements
- Improved German translation.

## Performance Improvements
-

## Community Improvements
-

## Dependencies
- Minimum version of PHP bumped from PHP 7.2.9 to PHP 8.0.2
- Laravel upgraded from 6.x LTS to 9.x
- Twig upgraded from 2.x to 3.x
- Minimum version of Laravel Tinker bumped to 2.7
- Minimum version of PHPUnit bumped to 9.5.8
- Minimum version of Mockery bumped to 1.4.4
- Symfony ugpraded from 4.x to 6.x
- Symfony/Yaml upgraded from 3.4 to 6.0
- Assetic upgraded from the modified embedded version of 1.4.0 to 3.0 as an external dependency.
