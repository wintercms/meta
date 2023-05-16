# Build 1.2.2 (WIP)

## UX/UI Improvements
- Added support for child themes and nested layouts, by defining a theme code in the `parent` property of a theme's configuration file (`theme.yaml`).
- Component assets stored in an `assets` directory within the component directory will now be mirrored by the `winter:mirror` command.
- The AJAX form validation feature [documented in Snowboard](https://wintercms.com/docs/snowboard/extras#ajax-validation) that was missed during the initial implementation of Snowboard is now included by default with the `extras` package.
- Lists can now be sorted by invisible columns.
- Tweaked sizing of the inputs for a `datepicker` field in `datetime` mode - the date input size has been slightly increased, and the time input size has been slightly decreased, to better fit their respective content.
- Removed the suggestion to install the Winter.Drivers plugin when using the `winter:install` command, as this plugin is now deprecated.
- Added ability to extend the `<head>` content in the Backend through a Backend partial by calling `Block::append('head', ...)`.
- Improved the pluralization of the file counts within folders in the Media Manager.

## API Changes
- A new configuration, `develop.debugSnowboard`, has been added to `config/develop.php`, to allow overriding if Snowboard debugging and console logging is enabled, independent of the `app.debug` setting.
- The `content` function in Twig now can return a boolean, thus allowing usage as a conditional for fallback content if a content file does not exist.
- The `Markdown` parser now uses the [CommonMark library](https://commonmark.thephpleague.com/) by the PHP League, as this library is already a Laravel dependency.
- A `$settingsCacheTtl` property may be provided for models that implement the `SettingsModel` behavior. This property accepts an integer and allows you to set the length of time (in seconds) that settings in this model will be cached for, defaulting to 1440 seconds (24 minutes).
- Added additional metadata properties such as last modification time and filesize to the `getList` method in the Media Manager widget.
- Added additional `mode` options for `mediafinder` fields to filter specific file types: `image`, `audio`, `video`, `document`, `file` and `all` (default).
- 

## Bug Fixes
- Fixed an issue with using `url()` paths in CSS files that are then compiled with the Asset Compiler.
- Fixed invalid HTML generation, such as missing attributes and values, for some form elements in the `Winter\Storm\Html\FormBuilder` class due to changes in the API signatures implemented through static testing. (https://github.com/wintercms/winter/issues/864)
- Improved compatibility with path symbol usage in the Asset combiner.
- Fixed the usage of POST arrays when using the original AJAX framework, which sometimes were incorrectly collated by the nested parent forms functionality implemented in Winter v1.2.0.
- Fixed `depends` usage in the Inspector widgets for `object` and `objectlist` fields.
- Fixed compilation and JavaScript issues in the `iconpicker` field introduced in Winter v1.2.1.
- Fixed the `themes` prefix to allow themes to localize the field attributes used in the "Customize theme" screen in the Backend.
- Fixed a missing use case for the `Log` facade in the CMS controller class.
- Fixed the type hinting for getting a theme's datasource which sometimes caused CMS pages to not load.
- Fixed incorrect usage of the `plugin:install` command inside the `winter:install` command, due to a change in the former command's parameters.
- Fixed incorrect URLs being returned by the `System\Models\File::getPublicPath()` method if the storage being used was not a local file storage.
- 

## Security Improvements
-

## Translation Improvements
- Improved Russian translations.
- Improved French translations.

## Performance Improvements
-

## Community Improvements
- Improved examples in documentation for extending forms via the `form.extendFieldsBefore` and `form.extendFields` events.
- Updated the `wikimedia/composer-merge-plugin` dependency to the latest version to allow for the `replace` configuration of dependencies to be merged together.
- The `\TestCase` alias has been set up to point to the correct base test class for unit tests, removing the need for adding a polyfill class in unit tests to support testing in both Winter v1.1 and v1.2. By extending this alias, unit tests should now work in both branches.

## Dependencies
-
