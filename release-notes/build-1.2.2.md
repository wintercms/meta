# Build 1.2.2 (WIP)

## UX/UI Improvements
- Component assets stored in an `assets` directory within the component directory will now be mirrored by the `winter:mirror` command.
- The AJAX form validation feature [documented in Snowboard](https://wintercms.com/docs/snowboard/extras#ajax-validation) that was missed during the initial implementation of Snowboard is now included by default with the `extras` package.
- Lists can now be sorted by invisible columns.

## API Changes
- A new configuration, `develop.debugSnowboard`, has been added to `config/develop.php`, to allow overriding if Snowboard debugging and console logging is enabled, independent of the `app.debug` setting.
- The `content` function in Twig now can return a boolean, thus allowing usage as a conditional for fallback content if a content file does not exist.
- The `Markdown` parser now uses the [CommonMark library](https://commonmark.thephpleague.com/) by the PHP League, as this library is already a Laravel dependency.
- A `$settingsCacheTtl` property may be provided for models that implement the `SettingsModel` behavior. This property accepts an integer and allows you to set the length of time (in seconds) that settings in this model will be cached for, defaulting to 1440 seconds (24 minutes).

## Bug Fixes
-

## Security Improvements
-

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
