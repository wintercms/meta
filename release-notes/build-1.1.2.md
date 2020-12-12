# Build 1.1.2 (WIP)

## UX/UI Improvements
- Fixed issue where the browser's number increment/decrement control would cover up the placeholder text in `type: number` inputs when hovered over or focused on.

## API Changes
- Added support for the `{colorpicker}` field in the Dynamic Syntax parser.
- The `availableColors` attribute can now be specified for `colorpicker` type variables in the Dynamic Syntax parser.

## Bug Fixes
- Fixed a duplicate AJAX call being fired when using the "Apply" or "Clear" buttons in a group filter.
- Fixed an exception thrown on viewing or logging into the Backend when attempting to load the backend localization files of a missing theme.
- Fixed issue where `/0` would return the result from `/`.
- Fixed issue where plugins with external dependencies referenced in their migration files would fail to install correctly via the `plugin:install` CLI command while installing normally in a web environment.
- The `listAllDirectories()` method in the `MediaLibrary` helper now correctly excludes paths and directories that are specified in the storage ignore rules configuration.
- Fixed issue where field options specified using a static method in the form of `options: "\Path\To\Class::staticMethod"` were not receiving the Form widget instance or the Field widget instance as per the documentation.

## Security Improvements
-

## Translation Improvements
- Improved Slovakian translations.

## Performance Improvements
-

## Community Improvements
- Added a new `EventFake` class to provide mocking and testing services for events in unit tests.

## Dependencies
-
