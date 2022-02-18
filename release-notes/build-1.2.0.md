# Build 1.2.0 (WIP)

## UX/UI Improvements
- Added support for autocompletion for all Winter provided CLI commands.
- Added `complete()` function to the `create:command` Command scaffolding for providing autocompletion in console commands. (run `artisan completion --help` to setup autocompletion in your terminal)
- Added autocompletion support to the following commands:
    - `plugin:disable $name`
    - `plugin:enable $name`
    - `plugin:refresh $name`
    - `plugin:rollback $name ROLLBACK_VERSION`
    -
- Changed recommended language mode for component partial files to `wintercms-twig` instead of `twig`.
- The `.env` file is now a first class citizen in Winter and configuration files refer to it by default. You can continue to run `winter:env` to generate a file pulling from your configuration to provide the default values.
- The default configuration for the testing environment now includes an override to store files generated / modified throughout the test suite in a folder under tests/storage instead of polluting your regular local storage folder with files from tests that failed to clean up after themselves well enough.
- Added `migrate` as an alias to `winter:up` to simplify transitioning to Winter from Laravel

## API Changes
- `server.php` is no longer needed in order for `artisan serve` to function; it can be removed.
- An application key is no longer provided by default, if your Winter instance is missing one just run `artisan key:generate` and one will be generated and set for you.
- Added `@snowboard.base`, `@snowboard.request`, `@snowboard.attr`, `@snowboard.extras` AssetCombiner aliases.
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
- `Winter\Storm\Support\Facades\Str` facade has been removed, use `Winter\Storm\Support\Str` directly instead.
- The base `ModuleServiceProvider` no longer needs a call to `parent::register($module)` in the `register()` method as route registration is now handled in the `boot()` method.
- The `ThemeInstall`, `ThemeRemove`, `ThemeList`, `ThemeUse`, & `ThemeSync` console commands have been moved from the System module to the CMS module.
- Removed the `getAdapter()` method from Storage disk instances
- Added `getPathPrefix()` and `setPathPrefix()` methods to Storage disk instances
- Fixed issue where running `winter:version --changes` would always display "We have detected the following modifications:" even when no modifications were detected.
- The signature for `$twig->loadTemplate()` has been changed, use `$twig->load()` instead.

## Bug Fixes
- `route:list` and `route:cache` now support module routes out of the box.
- Replaced usage of `{% filter %}` in the demo theme with `{% apply %}` instead.
- Fixed issue where the default CMS twig environment was unable to be extended or reused, resolve `twig.environment.cms` before it's used by the CMS in order to use or modify it.
- Fixed issue where calling `Twig::parse()` before doing anything that rendered Mail content (i.e. sending an email) would cause the Mail twig rendering to stop working.
- Fixed inconsistency where `CmsCompoundObject` instances were not using the default CMS twig environment.
- Removed requirement for a `Cms\Classes\Controller` instance on the `Cms\Twig\DebugExtension` making it easier to reuse elsewhere.
- `winter:version` will now only normalize file contents before hashing if the file is a valid text-based file which improves the reliability of change detection on Windows.
- `winter:passwd` now returns the status codes instead of using `exit($code)`

## Security Improvements
-

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
- Symfony/Yaml upgraded from 3.4 to 5.1
- Minimum version of Laravel Tinker bumped to 2.7
- Minimum version of PHPUnit bumped to 9.5.8
- Minimum version of Mockery bumped to 1.4.4
- Symfony ugpraded from 4.x to 6.x
