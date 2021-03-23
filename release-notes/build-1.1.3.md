# Build 1.1.3 (WIP)

## UX/UI Improvements
- Added support for choosing the default backend locale and timezone in `php artisan winter:install`.

## API Changes
- Added support for modifying the RichEditor's allowed attributes list through the EditorSettings in the backend
- Added support for lazy loading class aliases only when needed through the new `Winter\Storm\Support\ClassLoader->addAliases(['Real\Class' => 'Alias\For\Class'])` method.
- Added support for saving deferred bindings with pivot data.
- Added `Backend::makeCarbon($dateTime)` helper for setting the backend timezone on date values.
- Added support for Dependency Injection in console commands.
- Added support for `php artisan winter:util purge orphans` command that removes any `system_files` records that do not have matching files stored on the filesystem.
- Added support for `registerValidationRules` in the `Plugin.php` plugin registration file to register custom validation rules.
- Added support for specifying `min`, `max`, and `step` values on the `number` and `numberrange` List Filter scope types.

## Bug Fixes
- Fixed issue with Schedule->withoutOverlapping() by bringing the Halcyon MemoryRepository more inline with the parent class.
- Fixed an error thrown when using the "package:discover" command when `app.loadDiscoveredPackages` set to false, as the manifest was reset to `null` as opposed to an empty array.
- Fixed issue where tooltips set on the first column of the Lists widget were not working.
- Fixed issue where components that used dependency injection in their constructors would break in the backend.
- The RecordFinder FormWidget will now automatically determine what to use for the key column if the model used is not using the default of `id`. This used to be controlled by the undocumented `keyFrom` option on the recordfinder, but is now handled behind the scenes automatically.

## Security Improvements
- Improved password reset flow by no longer throwing an error message if the provided email address doesn't exist in the system.

## Translation Improvements
- Improved French translation.
- Improved Russian translation.
- Moved Media Manager `rename` and `move` action language keys to the backend module instead of the CMS module.

## Performance Improvements
-

## Community Improvements
- Documented the Lists widget's `perPageOptions` configuration property

## Dependencies
- Refactored the `Winter\Storm\Events\Dispatcher` class to extend and override the base Laravel Event Dispatcher rather than just duplicating and implementing the contract for greater compatibility with Laravel.
