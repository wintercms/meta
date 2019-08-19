# Build 459 (WIP):

## UX/UI Improvements:
- The theme Delete button is now hidden for the currently active theme as you cannot delete the active theme anyways.
- Added a warning to the System Status dashboard ReportWidget when debug mode is enabled as debug should never be enabled in production.
- Invalid menu items now throw a ValidationException when debug mode is enabled and log and error instead when debug is disabled.
- Added support for Repeater item titles to be pulled from dropdown field types.
- Added the Validation trait to model stubs when calling `create:model`.

## API Changes:
- When setting relationship values model mutator methods (`'set' . $attribute . 'Attribute'`) are now taken into account meaning that you can control how specific relationship values are set by defining a custom mutator method for the relationship.
- Added `getReportWidgets()` method to `Backend\Classes\WidgetManager` to return the protected array of currently registered report widgets
- Custom theme data stored in `cms_theme_data` is now removed when the theme it belongs to is deleted.
- Added `develop.decompileBackendAssets` configuration flag to decompile the backend assets in order to simplify making changes to backend asset files for the purpose of making PRs to the OctoberCMS core.
- Switched parsing of stub files for the generator commands to use Twig instead of basic `str_replace()`, this will enable more complex stub files

## Bug Fixes:
- Fixed issue where the `TagList` FormWidget in `mode: relation` wasn't respecting relationship constraints (`conditions` and `scope`) set on the relationship definition.

## Security Improvements
-

## Translation Improvements:
- Improved Arabic translation

## Performance Improvements:
-

## Community Improvements:
- Added documentation on keeping local forks of the OctoberCMS codebase up to date with upstream.

## Dependencies
- Updated to v1.8.0 of Spectrum.js (Note: October was already using 1.8.0, however jQuery API updates were made without the vendor tagging a new release)