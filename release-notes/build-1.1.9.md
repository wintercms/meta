# Build 1.1.9 (WIP)

## UX/UI Improvements
-

## API Changes
- Dependency checking and management for Snowboard plugins has been improved. Singletons that have a `ready` callback will not be fired until dependencies are loaded.
- Added a `flash.create` and `flash.remove` global event in Snowboard to listen when a flash message is created and removed, respectively.
- Added URL handling and base URL detection in Snowboard via the `Snowboard.url()` plugin.
- Added `sortable` property to the Repeater FormWidget, defaults to `true`.
- Added a `mix:update` command to allow updating of Node dependencies for Mix assets.
- Added support for `type: nestedform` fields to the `ThemeData` theme customization forms.

## Bug Fixes
- Improved support for read-only filesystems by using the Storage facade to handle the disabled plugins cache file instead of directly interacting with the local disk and checking if the local filesystem is writable before attempting to create the temporary directory required by the `UpdateManager`.
- Fixed the System Status dashboard widget on read-only filesystems.
- Fixed issue where calling `Snowboard.request()` with the element parameter set to false or null would fail.
- Fixed issue where changes made to `$this->vars` in a Partial's PHP code section wouldn't be available in the Twig section.
- Fixed issue where a Snowboard plugin that had been removed could not be re-added.
- Backported a fix from the 1.2 branch which resolves timeout issues with the `mix:install` command.
- Fixed issue where using the `useRelationCount` option with a relation in a List widget would not retrieve the count if the relation name was not snake-cased.

## Security Improvements
- Improved reliability of the CMS Safe Mode feature. See https://github.com/wintercms/winter/security/advisories/GHSA-q37h-jhf3-85cj for more information

## Translation Improvements
- Improved German translation
- Improved Spanish translation

## Performance Improvements
-

## Community Improvements
- Fixed file language hinting for backend controller views for VS Code

## Dependencies
- The Winter core modules now report via composer that they replace the associated version of the October core modules to improve compatibility with the October ecosystem.
