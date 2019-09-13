# Build 459:

## UX/UI Improvements:
- The theme Delete button is now hidden for the currently active theme as you cannot delete the active theme anyways.
- Added a warning to the System Status dashboard ReportWidget when debug mode is enabled as debug should never be enabled in production.
- Invalid menu items now throw a ValidationException when debug mode is enabled and log an error instead when debug is disabled.
- Added support for Repeater item titles to be pulled from dropdown field types.
- Added the Validation trait to model stubs when calling `create:model`.
- Made the CodeEditor fullscreen button easier to see by increasing the contrast.

## API Changes:
- When setting relationship values model mutator methods (`'set' . $attribute . 'Attribute'`) are now taken into account meaning that you can control how specific relationship values are set by defining a custom mutator method for the relationship.
- Added `getReportWidgets()` method to `Backend\Classes\WidgetManager` to return the protected array of currently registered report widgets
- Custom theme data stored in `cms_theme_data` is now removed when the theme it belongs to is deleted.
- Added `develop.decompileBackendAssets` configuration flag to decompile the backend assets in order to simplify making changes to backend asset files for the purpose of making PRs to the OctoberCMS core.
- Switched parsing of stub files for the generator commands to use Twig instead of basic `str_replace()`, this will enable more complex stub files

## Bug Fixes:
- Fixed issue where the `TagList` FormWidget in `mode: relation` wasn't respecting relationship constraints (`conditions` and `scope`) set on the relationship definition.
- Fixed issue where using the `::class` magic constant in database migrations would cause them to break due to flawed parsing logic.
- Fixed use of Storage::url() for local disks that haven't been configured correctly
- Moved the translation for plugin's "By $author" text in the plugin update view to the System module instead of the CMS module to support installations without the CMS module enabled or installed.
- Removed old "Holly Hack" for IE5-IE7 support, we don't support those browsers anymore.
- Fixed Theme importing/exporting that was broken as of 457-458.
- Fixed issue where the session expiring would throw a vague exception when attempting to check the CSRF token instead of just throwing a general CSRF invalid error message.
- Fixed issue where multiple instances of the PermissionEditor could not exist on a single page.

## Translation Improvements:
- Improved Arabic translation

## Performance Improvements:
- The file extension has been added to the end of asset combiner URLs (ex. /combine/asqw3ljkqw421323.js or /combine/lkj23jlk13j1l.css) in order to allow CDNs to more easily identify the URL as cacheable to improve overall site performance.

## Community Improvements:
- Added documentation on keeping local forks of the OctoberCMS codebase up to date with upstream.
- Improved the CONTRIBUTING.md guide
- Added security policy
- Added documentation for testing pull requests

## Dependencies
- Updated to v1.8.0 of Spectrum.js (Note: October was already using 1.8.0, however jQuery API updates were made without the vendor tagging a new release)