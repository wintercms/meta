# Build 1.1.2 (WIP)

> **NOTE:** As of v1.1.2, the core maintainer team has left October CMS and forked the project into Winter CMS.

## UX/UI Improvements
- Fixed issue where the browser's number increment/decrement control would cover up the placeholder text in `type: number` inputs when hovered over or focused on.
- Added ability to select the default backend locale when running the `october:install` command

## API Changes
- Added support for the `{colorpicker}` field in the Dynamic Syntax parser.
- The `availableColors` attribute can now be specified for `colorpicker` type variables in the Dynamic Syntax parser.
- Added new `getRelationTypeDefinitions` and `getRelationTypeDefinition` methods to models to query relationship definitions through methods as opposed to interacting with the relation properties directly.
- The "Customize" button is now disabled for all themes that are not the currently active theme.

## Bug Fixes
- Fixed a duplicate AJAX call being fired when using the "Apply" or "Clear" buttons in a group filter.
- Fixed an exception thrown on viewing or logging into the Backend when attempting to load the backend localization files of a missing theme.
- Fixed issue where `/0` would return the result from `/`.
- Fixed issue where plugins with external dependencies referenced in their migration files would fail to install correctly via the `plugin:install` CLI command while installing normally in a web environment.
- The `listAllDirectories()` method in the `MediaLibrary` helper now correctly excludes paths and directories that are specified in the storage ignore rules configuration.
- Fixed issue where field options specified using a static method in the form of `options: "\Path\To\Class::staticMethod"` were not receiving the Form widget instance or the Field widget instance as per the documentation.
- Fixed issue introduced in Laravel 5.7 where eager loading `File` relationships on PostgreSQL would fail with the message "Varchar <> Integer comparison is not allowed".
- Fixed issue where having safeMode enabled when editing a CMS CompoundObject with different line endings from the user's browser (i.e. `\r` vs `\r\n`) would cause the safe mode protection to unnecessarily trigger (preventing any changes to non-protected properties from being saved) because the user's browser would modify the original line endings.
- Fixed an issue with integers being used as keys for the options in the checkbox list.
- Fixed an issue with syncing belongToMany relationships introduced in v1.1.1.
- Fixed an issue where the user-provided password for the default admin account during `october:install` was not being respected and was instead always being set to a random string of characters as if no password had been provided.
- Fixed an issue where the ImageResizer was always provided absolute URLs instead of respecting the value of `cms.linkPolicy`.
- Fixed an issue where calling `detach()` on a BelongsToMany relationship where a scope was defined on the relationship would fail.

## Security Improvements
- Tightened up the Twig SecurityPolicy. Calling `insert()`, `update()`, `delete()` methods on all PHP objects are now blocked from within Twig, data modifications should not be done at the view layer. If absolutely necessary, consider firing a view event instead.
- Added a new config value (`app.trustedHosts`) to protect against [host header poisoning](https://portswigger.net/web-security/host-header). The following values can be used: the default of `true` will allow only the naked and `www` versions of `app.url` as trusted hosts, `false` will disable the feature (except on the backend password reset flow), and finally an array of trusted host patterns.
- Session identifiers are now invalidated on logging out instead of just flushed.

## Translation Improvements
- Improved Slovakian translation.
- Improved Hungarian translation.
- Improved Brazilian Portuguese translation.
- Improved Dutch translation.

## Performance Improvements
-

## Community Improvements
- Added a new `EventFake` class to provide mocking and testing services for events in unit tests.
- Fixed the order of parameters in the docblock for the `mailer.beforeAddContent` event.

## Dependencies
- Updated Pikaday to 1.8.2
- Switched back to the source repository for the `wikimedia/composer-merge-plugin` as Composer 2.0 support has fully arrived. Update your `composer.json` files to require `"wikimedia/composer-merge-plugin": "~2.0.1"`
