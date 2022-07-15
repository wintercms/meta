# Build 1.2.0 (WIP)

See the [Upgrade Guide](https://github.com/wintercms/meta/blob/master/l9-upgrade-notes.md) for a quick highlight of any potentially required changes in your code in order to be compatible with Winter CMS v1.2+. Although the upgrade should be relatively painless it is still worth taking a quick look to verify that you are not affected by any of the relatively few breaking changes.

Due to the significant number of changes in 1.2, they are grouped by section rather than category for this release note.

- [Dependencies](#dependencies)
- [Community Improvements](#community-improvements)
- [CLI & Console Commands](#console)
- [Project Configuration & Helper Files](#config)
- [Testing](#testing)
- [Plugin Manager](#plugins)
- [Backend UI & UX](#backend)
- [Media Manager & Image Resizing](#media)
- [Themes](#themes)
- [Twig](#twig)
- [Events](#events)
- [Database](#database)
- [Filesystem](#filesystem)
- [Modules](#modules)
- [Internals](#internals)



<a name="dependencies"></a>
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



<a name="community-improvements"></a>
## Community Improvements

Over the past year as we have been working on the Laravel 9 upgrade we have released a number of plugins, themes, and development tools designed to further enhance the Winter CMS developer experience.

- [First Party Plugins](#community-plugins)
- [First Party Themes](#community-themes)
- [VS Code Extension](#community-vscode)

<a name="community-plugins"></a>
### First Party Plugins:

The following first party plugins were released / revamped:

- [Winter.TailwindUI](https://github.com/wintercms/wn-tailwindui-plugin) - TailwindUI-based skin for the backend.
- [Winter.Search](https://github.com/wintercms/wn-search-plugin) - Enables full-text search capabilities in Winter.
- [Winter.Redirect](https://github.com/wintercms/wn-redirect-plugin) - Manage redirects.
- [Winter.Docs](https://github.com/wintercms/wn-docs-plugin) - Manages & displays documentation from various sources within your Winter projects.
- [Winter.Matomo](https://github.com/wintercms/wn-matomo-plugin) - Integrates the open source Matomo Analytics platform into Winter.
- [Winter.DriverAWS](https://github.com/wintercms/wn-driveraws-plugin) - Driver plugin that adds support for AWS to Winter.
- [Winter.DriverMailgun](https://github.com/wintercms/wn-drivermailgun-plugin) - Driver plugin that adds support for Mailgun to Winter.
- [Winter.DriverMandrill](https://github.com/wintercms/wn-drivermandrill-plugin) - Driver plugin that adds support for Mandrill to Winter.
- [Winter.DriverPostmark](https://github.com/wintercms/wn-driverpostmark-plugin) - Driver plugin that adds support for Postmark to Winter.
- [Winter.DriverSendGrid](https://github.com/wintercms/wn-driversendgrid-plugin) - Driver plugin that adds support for SendGrid to Winter.
- [Winter.DriverSparkPost](https://github.com/wintercms/wn-driversparkpost-plugin) - Driver plugin that adds support for SparkPost to Winter.

<a name="community-themes"></a>
### First Party Themes:

The following first party themes were released:

- [Nabu](https://github.com/wintercms/wn-nabu-theme) - Theme designed for documentation sites using the powerfull Winter.Docs & Winter.Search plugins.
- [Workshop](https://github.com/wintercms/wn-workshop-theme) - TailwindCSS-built theme for testing first party plugins.

<a name="community-vscode"></a>
### VSCode Extension:

The [official Winter CMS VSCode extension](https://marketplace.visualstudio.com/items?itemName=wintercms.winter-cms) was released which provides code completion and syntax highlighting for Winter CMS projects.



<a name="console"></a>
## CLI & Console Commands

A number of improvements have been made to the console commands available out of the box with Winter as well as the developer experience for working with the CLI in general. In addition to these improvements, the Console documentation has been updated and enhanced, [click here to read the docs](https://github.com/wintercms/docs/blob/wip/1.2/console-introduction.md).

- [Autocompletion](#console-autocompletion)
- [Improved Support for Laravel-provided commands](#console-laravel)
- [New Winter\Storm\Console\Command base class and helpers](#console-base-class)
- [Scaffolding Improvements](#console-scaffolding)
- [Bug Fixes](#console-bug-fixes)

<a name="console-autocompletion"></a>
### Autocompletion

- Added support for autocompletion for all Winter provided CLI commands.
- Added `complete()` function to the `create:command` Command scaffolding for providing autocompletion in console commands. (run `artisan completion --help` to setup autocompletion in your terminal)
- Added autocompletion support to the following commands:
    - `plugin:disable $name`
    - `plugin:enable $name`
    - `plugin:refresh $name`
    - `plugin:rollback $name $rollbackVersion`
    - `winter:passwd $username` (last 20 updated backend users)

<a name="console-laravel"></a>
### Improved Support for Laravel provided commands

- Added `migrate` as an alias to `winter:up` to simplify transitioning to Winter from Laravel
- Laravel's migration commands have been removed / aliased to the relevant Winter commands as they did not function with Winter and never have.
- Version number reported by `artisan --version` will now include `Winter CMS`.
- `route:list` and `route:cache` now support module routes out of the box.
- Fixed issue where the `key:generate` command wouldn't set the `APP_KEY` value in the `.env` file if the `.env` file didn't exist yet.

<a name="console-base-class"></a>
### New Winter\Storm\Console\Command base class and helpers

- Added `Winter\Storm\Console\Command` base class that adds helpers for making it easier for commands to implement suggested values for autocompletion.
- Added `alert()` helper to the Winter `Command` base class that improves on the Laravel default by adding support for wrapping long alert messages to multiple lines.
- Added `Winter\Storm\Console\Traits\ConfirmsWithInput` trait provides the `confirmWithInput($message, $requiredInput)` method to require the user to input the required input string in order before proceeding with running the command.
- Added `Winter\Storm\Console\Traits\ProcessesQuery` trait that provides a `processQuery($query, $callback, $chunkSize, $limit)` method that simplifies the process of processing large numbers of records in console commands by handling creating and updating a progress bar, chunking the provided query by the provided chunk size and limit parameters, running the callback for each record, and gracefully handling any exceptions thrown during the processing of records.

<a name="console-scaffolding"></a>
### Scaffolding Improvements

- Added `create:job Author.Plugin JobName` scaffolding console command to create an initial Job class
- Added new `scaffold` argument to `create:theme` command, defaults to `less`; also supports `tailwind`.
- Moved all scaffolding commands out of `Winter\Storm` and into their relevant Modules (`Backend`, `CMS`, & `System`).
- Added `$nameFrom` property and `getNameInput()` method to the `Winter\Storm\Scaffold\GeneratorCommand` to enable checking for reserved names when generating code via scaffolding commands. Also made some method signature type hint changes to the class, be sure to review and apply them accordingly in any custom uses of that base class.
- Removed `getPluginIdentifier()` method from the `Winter\Storm\Scaffold\GeneratorCommand` class and added a new base class for scaffolding resources that are specific to plugins: `System\Console\BaseScaffoldCommand`.
- Added support for autocompletion of the `plugin` argument for scaffolders that extend `System\Console\BaseScaffoldCommand`.
- Added `System\Console\Traits\HasPluginInput` trait that provides helpers for when a console command interacts with plugin names as input arguments.
- Added support for generating localization messages by calling a `getLangKeys()` method defined on the scaffolding command during the execution process. This method can use the `$this->vars` property and `$this->laravel->getLocale()` method to return an associative array of message keys without the author prefix and their values for the current locale.
- Added several helpers in the scaffolding template files:
    - `plugin_id` -> lowercase version of a plugin's identifier
    - `plugin_code` -> Studly case version of the plugin's identifier
    - `plugin_url` -> `author/plugin`, used in `Backend::url()` calls
    - `plugin_folder` -> `author/plugin`, used when generating paths to files with the `$` plugins directory path symbol or the `~` application path symbol.
    - `plugin_namespace` -> Studly case version of the plugin's identifier in namespace form (i.e. `Author\Plugin`)

<a name="console-bug-fixes"></a>
### Bug Fixes

- Added ability for the `mix:watch` command to clean up after itself when terminated with SIGTERM.
- `winter:version` will now only normalize file contents before hashing if the file is a valid text-based file which improves the reliability of change detection on Windows.
- Fixed issue where running `winter:version --changes` would always display "We have detected the following modifications:" even when no modifications were detected.
- `winter:passwd` now returns the status codes instead of using `exit($code)`
- Fixed issue where if the underlying data behind a datasource changes through manual intervention (either in the database or the filesystem) before running `theme:sync` it wasn't being detected by the `theme:sync` command.
- The `ThemeInstall`, `ThemeRemove`, `ThemeList`, `ThemeUse`, & `ThemeSync` console commands have been moved from the System module to the CMS module.



<a name="config"></a>
## Project Configuration & Helper Files

- An application key is no longer provided by default, if your Winter instance is missing one just run `artisan key:generate` and one will be generated and set for you.
- The `.env` file is now a first class citizen in Winter and configuration files refer to it by default. You can continue to run `winter:env` to generate a file pulling from your configuration to provide the default values.
- Changed recommended language mode for component partial files to `wintercms-twig` instead of `twig` in `.vscode/extensions.json`
- `server.php` is no longer needed in order for `artisan serve` to function; it can be removed.
- Removed `varcharmax` as a configuration option for `mysql` database connections.
- Added `app.tempPath` configuration option to set the application's temporary path.



<a name="testing"></a>
## Testing

- The default configuration for the testing environment now includes an override to store files generated / modified throughout the test suite in a folder under system/tests/storage instead of polluting your regular local storage folder with files from tests that failed to clean up after themselves well enough.
- PHPUnit arguments can now be passed to the `winter:test` command by first separating the arguments meant for Winter and the PHPUnit arguments / options with a `--`. Example: `winter:test --module=system -- --filter=ImageResizerTest`
- Unit tests have been moved from the project's `tests/` folder into individual `tests/` folders under each core module. Modules can now be tested individually by running `winter:test` with the `-m` or `--module` options (ex. `winter:test -m cms -m system -m backend`)
- The base `TestCase` & `PluginTestCase` classes are now namespaced under the System module, extend `System\Tests\Bootstrap\TestCase` & `System\Tests\Bootstrap\PluginTestCase` instead.



<a name="plugins"></a>
## Plugin Manager

- The PluginManager logic now runs off of a "flag" system internally allowing for greater insight into why a particular plugin is disabled and greater control over programmatically disabling / enabling plugins at runtime via the new `PluginManager::DISABLED_REQUEST` flag. The following changes were made the `System\Classes\PluginManager`'s public API:
    - Removed the following methods:
        - `bindContainerObjects()`: No replacement.
        - `clearDisabledCache()`: Use `clearFlagCache()` instead if required.
        - `registerReplacedPlugins()`: Now handled as a part of `loadPluginFlags()`.
    - Added the following methods:
        - `loadPluginFlags()`: Loads the plugin flags (disabled & replacement states) from the cache regenerating them if required.
        - `clearFlagCache()`: Resets the plugin flag cache
        - `getPluginFlags(PluginBase|string $plugin): array`: Retrieves any flags that are currently set for the provided plugin.
        - `freezePlugin(PluginBase|string $plugin)`: Flags the provided plugin as "frozen" (updates cannot be downloaded / installed).
        - `unfreezePlugin(PluginBase|string $plugin)`: "Unfreezes" the provided plugin, allowing for updates to be performed.
- Added `checkDependencies()` method to the `PluginBase` class to handle checking if the plugin's dependencies are present.
- Improved PluginManager performance & reliability by using the Cache system instead of a local JSON file for managing plugin flags.
- Improved performance of projects using plugins with `plugin.yaml` files by caching the parsed results of said files.
- Changed `System\Classes\VersionManager->getDatabaseHistory($pluginCode)` from protected to public.
- Fixed issue where plugins using `v` in their version identifiers would sometimes have issues when migrating between versions.



<a name="backend"></a>
## Backend UI & UX

- Icon library updated from Font Awesome version 4 to 6, bringing over 1,300 new icons.
- Added improved UX for invalid date values being provided to the datepicker FormWidget.
- Backend template files (layouts, views, & partials) now use the `.php` extension which reduces confusion about what templating language is used for backend template files. `.htm` files are still supported, but not recommended.
- Fixed support for morphOne/hasOne relations in FormModelSaver
- Fixed issue where paths returned by the UploadableWidget could have two leading directory separators.
- Improved German translation.
- Improved Russian translation.



<a name="media"></a>
## Media Manager & Image Resizing

- Made it easier to track down issues with the `ImageResizer` class by only removing the resizer configuration from the Cache after the resizer has been successfully instantiated.
- Added `ImageResizer::getDefaultDisk()` method to get the default Storage disk used by the ImageResizer
- Added `(ImageResizer)->getDisk()` method to get the disk for the currently active image
- Made `getMediaPath($path)` and `getStorageDisk()` on `System\Classes\MediaLibrary` public (previously protected)
- Made the `getStorageDisk()` and `getMediaPath()` methods on `System\Classes\MediaLibrary` public instead of protected.
- Improved MediaManager performance by using the ImageResizer's lazy resized images for thumbnails.
- Improved MediaManager & ImageResizer support for read-only environments (i.e. Laravel Vapor)
- Resized images are now cached by the modified time of their source image allowing replacements of the source image to trigger the resizing to regenerate based on the new source image.



<a name="themes"></a>
## Themes

- Added support for generating a TailwindCSS based theme via `artisan create:theme mytheme tailwind`
- Added `@snowboard.base`, `@snowboard.request`, `@snowboard.attr`, `@snowboard.extras`, & `@snowboard.extras.css` AssetCombiner aliases.
- Fixed issue where the `Cms\Classes\Page` `isActive` property wasn't being set if the URL was set to `/` and the currently requested URL was the home page.
- Added support for `multiple: bool` property on `type: fileupload` fields in the Theme Customization section to choose between an `attachOne` and `attachMany` relationship.



<a name="twig"></a>
## Twig

- The following Twig environments are now registered by the application and can be resolved by calling `App::make($environmentName);`:
    - `twig.environment` The default System TwigEnvironment, is used by the `Twig::parse()` parser
    - `twig.environment.mailer` The Mailer TwigEnvironment, used by the `MailManager` class when rendering emails
    - `twig.environment.cms` The CMS TwigEnvironment, used by the CMS when rendering CMS templates
- Added the `System\Classes\MarkupManager::makeBaseTwigEnvironment(TwigLoader $loader, array $options)` static helper method that returns the basic `TwigEnvironment` that should be used by any custom Twig implementation in Winter CMS (i.e. applies the default security policy and `SystemTwigExtension`).
- Removed the `transaction()`, `beginTransaction()`, and `endTransaction()` methods from `System\Classes\MarkupManager` since "markup transactions" was a hacky workaround originally implemented due to global polution of the single Twig environment. This is no longer required with the use of multiple, separate twig environments.
- Added support for the `{% spaceless %}` and `{% filter %}` Twig tokens to the core as Twig v3 removed them; it is recommended to avoid using them however.
- The signature for `$twig->loadTemplate()` has been changed, use `$twig->load()` instead.
- Replaced usage of `{% filter %}` in the demo theme with `{% apply %}` instead.
- Fixed issue where the default CMS twig environment was unable to be extended or reused, resolve `twig.environment.cms` before it's used by the CMS in order to use or modify it.
- Fixed issue where calling `Twig::parse()` before doing anything that rendered Mail content (i.e. sending an email) would cause the Mail twig rendering to stop working.
- Fixed inconsistency where `CmsCompoundObject` instances were not using the default CMS twig environment.
- Removed requirement for a `Cms\Classes\Controller` instance on the `Cms\Twig\DebugExtension` making it easier to reuse elsewhere.



<a name="events"></a>
## Events

- Added two new events (`system.beforeRoute` and `system.route`) that fire before and after the system route registration respectively and moved the registration of the Backend and CMS module routes to be after the system route registration. The CMS module's routes should now always be the last routes registered regardless of what happens.
- The `backend.layout.extendHead` event now passes `auth` or `default` as the value for `layout` instead of `auth.htm` or `default.htm`.
- Fixed issue where attempting to interact with a Model instance before the DatabaseServerProvider boot() method was called would prevent any "nice" model events from actually working.
- Removed `translator.beforeResolve` event, use `Lang::set($key, $value, $locale)` instead.



<a name="database"></a>
## Database

- Added support for [anonymous migrations](https://laravel-news.com/laravel-anonymous-migrations) and made them the default when creating new migrations with `artisan create:model`.
- Added `add{$RelationType}Relation($name, $config)` methods to the `HasRelationships` trait that make it easier to dynamically add new relationships to existing model classes.
- The pivot model for a `morphTo` relation now uses the `Winter\Storm\Database\MorphPivot` class, similar to Laravel's own `MorphPivot` class. If you wish to use a custom pivot model for a `morphTo` relation, the pivot model must extend this class.
- Added `Winter\Storm\Database\Traits\ArraySource` trait that allows a model to be created, queried and managed from arbitrary data as opposed to a database table.



<a name="filesystem"></a>
## Filesystem

- Removed the `getAdapter()` method from Storage disk instances
- Added `getPathPrefix()` and `setPathPrefix()` methods to Storage disk instances



<a name="modules"></a>
## Modules
- Module route registration should no longer require being wrapped in `App::before()` to support plugin's overriding them
- The base `ModuleServiceProvider` no longer needs a call to `parent::register($module)` in the `register()` method as route registration is now handled in the `boot()` method.



<a name="internals"></a>
## Internals

- `Winter\Storm\Support\Facades\Str` facade has been removed, use `Winter\Storm\Support\Str` directly instead.
- `Symfony\Component\Debug\Exception\FatalErrorException` has been removed, use `Symfony\Component\ErrorHandler\Error\FatalError` instead.
- Facades must return string keys rather than objects (See https://github.com/laravel/framework/pull/38017)
- Changed how YAML processors (added in v1.1.3) work; preprocessors are now only engaged if parsing the provided contents throws an exception.
- The SchemaBuilder is now bound to `db.schema` instead of only resolved directly through the `Schema` facade.
- Added `Winter\Storm\Parse\EnvFile` parsing class for handling modifying the contents of environment (`.env`) files through PHP.
- Added `Winter\Storm\Parse\PHP\ArrayFile` parsing class for handling modifying the contents of Array Files (PHP config & localization files that return a single array and are used for storing data). The `Winter\Storm\Config\ConfigWriter` class has been rewritten to use the `ArrayFile` parser internally.
- The load order of deferred Service Providers has been changed slightly, now the application will be made aware of the existence of deferred providers before it begins to register the eager loaded providers to allow for use of the deferred providers within the registration of the eager loaded providers. Actually doing so is still not recommended, but it was required for core internals of the PluginManager to perform better. See https://github.com/laravel/framework/pull/38724 & https://github.com/wintercms/storm/pull/86 for more details.
