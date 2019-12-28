# Build 463 (WIP):

## UX/UI Improvements:
- Fixed display of checkbox lists when quickselect is selected.
- Added new `october:passwd` Artisan command to change the password of a Backend user through the command-line.

## API Changes:
- `System\Classes\PluginManager->sortByDependencies()` is now deprecated as plugins are now sorted by key & dependencies by default.

## Bug Fixes:
- Added support for tab lazy loading to all forms of tabs, not just primary tabs.
- Fixed hard coded Form widget alias in the recently added tab lazy-loading functionality.
- Fixed support for Laravel's Builder::paginate() signature `paginate($perPage, $columns, $pageName, $currentPage)` in addition to October's `paginate($perPage, $currentPage, $columns, $pageName)`

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-
