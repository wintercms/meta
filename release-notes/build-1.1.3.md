# Build 1.1.3 (WIP)

## UX/UI Improvements
- Added support for choosing the default backend locale and timezone in `php artisan winter:install`.
- Controller scaffolding now uses the default backend localization keys for the default titles in the FormBehavior config instead of hardcoded English strings

## API Changes
- Added support for modifying the RichEditor's allowed attributes list through the EditorSettings in the backend
- Added support for lazy loading class aliases only when needed through the new `Winter\Storm\Support\ClassLoader->addAliases(['Real\Class' => 'Alias\For\Class'])` method.
- Added support for saving deferred bindings with pivot data.
- Added `Backend::makeCarbon($dateTime)` helper for setting the backend timezone on date values.
- Added support for Dependency Injection in console commands.
- Added support for `php artisan winter:util purge orphans` command that removes any `system_files` records that do not have matching files stored on the filesystem.
- Added support for `registerValidationRules` in the `Plugin.php` plugin registration file to register custom validation rules.
- Added support for specifying `min`, `max`, and `step` values on the `number` and `numberrange` List Filter scope types.
- Added support for translator namespace aliases by adding `Lang::registerNamespaceAlias('real.namespace', 'aliased.namespace')`.
- Added support for aliasing entire namespaces in the class loader via the new `Winter\Storm\Support\ClassLoader->addNamespaceAliases(['Real\Namespace' => 'Aliased\Namespace'])` method.
- Added support for pre and post processing of YAML being parsed which should pave the way for supporting YAML v4
- Added support for array views to the MailFake class
- Added support for HTTP HEAD requests from the `Http` utility.
- Added boolean `$ok` indicator to the `Http` utility to indicate if the last response was successful (ie. an HTTP 2xx response code was returned)

## Bug Fixes
- Fixed issue with Schedule->withoutOverlapping() by bringing the Halcyon MemoryRepository more inline with the parent class.
- Fixed an error thrown when using the "package:discover" command when `app.loadDiscoveredPackages` set to false, as the manifest was reset to `null` as opposed to an empty array.
- Fixed issue where tooltips set on the first column of the Lists widget were not working.
- Fixed issue where components that used dependency injection in their constructors would break in the backend.
- The RecordFinder FormWidget will now automatically determine what to use for the key column if the model used is not using the default of `id`. This used to be controlled by the undocumented `keyFrom` option on the recordfinder, but is now handled behind the scenes automatically.
- Reverted "Fixed issue introduced in Laravel 5.7 where eager loading `File` relationships on PostgreSQL would fail with the message "Varchar <> Integer comparison is not allowed"" introduced in 1.1.2 since it was causing issues when strict typing was enabled.
- Fixed an issue where `PluginManager->getRegistrationMethodValues()` would attempt to call protected methods on PHP 7.4.
- Improved Media Library path validation logic by allowing `//` but not allowing `://` to account for poorly constructed paths that are still technically valid.
- Fixed issue where sending emails using the Laravel Notification system could cause an exception in the System module when it attempted to extend a view instance while it was expecting a view string reference.
- Fixed issue where a TagList field that is disabled or readOnly would fail to correctly render if the value was an array.
- Added branching support for `winter:version`, different version branches (1.0, 1.1, etc) can now be correctly identified.

## Security Improvements
- Improved password reset flow by no longer throwing an error message if the provided email address doesn't exist in the system.

## Translation Improvements
- Improved French translation.
- Improved Russian translation.
- Improved Dutch translation.
- Moved Media Manager `rename` and `move` action language keys to the backend module instead of the CMS module.

## Performance Improvements
-

## Community Improvements
- Documented the Lists widget's `perPageOptions` configuration property

## Dependencies
- Refactored the `Winter\Storm\Events\Dispatcher` class to extend and override the base Laravel Event Dispatcher rather than just duplicating and implementing the contract for greater compatibility with Laravel.
- Updated from `symfony/yaml` v3.4 to `symfony/yaml` v4.4 and added a default preprocessor to automatically fix breaking changes between v3 and v4 of the symfony/yaml package.
