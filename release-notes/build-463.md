# Build 463 (WIP):

## UX/UI Improvements:
- Fixed display of checkbox lists when quickselect is selected.
- Added new `october:passwd` Artisan command to change the password of a Backend user through the command-line.
- Secondary branding colour is now applied to the active media filter in the MediaManager widget
- Lists can now disable the click event by applying the `nolink` CSS class to table row (TR) elements in addition to table data elements (TD) elements.

## API Changes:
- `System\Classes\PluginManager->sortByDependencies()` is now deprecated as plugins are now sorted by key & dependencies by default.
- Changed the `October\Rain\Database\Builder->simplePaginate()` signature to match `paginate()` (`$perPage, $currentPage, $columns, $pageName`)
- Added `engine => InnoDB` to the default `mysql` database driver configuration
- Added support for `varcharmax` to the `mysql` database driver configuration to specify the default length used for varchar / string columns when running migrations. If using `utf8mb4` on MySQL < 5.7 or MariaDB < 10.2 this should be set to 191, newer versions can be safely set to 255 however.
- Translator `trans` and `transChoice` method arguments have changed to match the Laravel 5.5 base package.

## Bug Fixes:
- Fixed the LESS compiler using PHP 7.4 that was previously throwing an error.
- Added support for tab lazy loading to all forms of tabs, not just primary tabs.
- Fixed hard coded Form widget alias in the recently added tab lazy-loading functionality.
- Fixed support for Laravel's Builder::paginate() signature `paginate($perPage, $columns, $pageName, $currentPage)` in addition to October's `paginate($perPage, $currentPage, $columns, $pageName)`. Additionally fixed support for Laravel's `simplePaginate()` signature.
- Fixed issue where errors thrown during the page processing of the RelationController would be silently consumed without being reported to the user.
- Fixed issue where popups can still be interacted with when they are in a loading state using `data-popup-load-indicator`.

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
-

## Community Improvements:
- Updated minimum required PHP version for the installer to match Build 472's minimum of 7.0.8

## Dependencies
-
