# Build 1.2.0 (WIP)

## UX/UI Improvements
- Added support for autocompletion for all Winter provided CLI commands.
- Added `complete()` function to the `create:command` Command scaffolding for providing autocompletion in console commands. (run `artisan completion --help` to setup autocompletion in your terminal)
- Changed recommended language mode for component partial files to `wintercms-twig` instead of `twig`.

## API Changes
- `server.php` is no longer needed in order for `artisan serve` to function; it can be removed.
- Added `@snowboard.base`, `@snowboard.request`, `@snowboard.attr`, `@snowboard.extras` AssetCombiner aliases.

## Bug Fixes
-

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
