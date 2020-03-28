# Build 466 (WIP)

## UX/UI Improvements
-

## API Changes
- Menu items controlled by `NavigationManager` are now objects, and `$manager->getMainMenuItem($owner, $code)` has been added to make it easier to manipulate existing menu items without having to deregister and reregister menu items to apply changes.
- The `postbackHandler` property for DataTable form widgets now defaults to `null` - the widget will interpret a `null` value as to detect the save handler for the form that contains the widget (this is usually `onSave`, the old default value, but it will now detect other handlers such as those used by the relation controller).
- The `getParameter` method in `Cms\Classes\Router` is now correctly type-hinted.
- External parameters may now use dot notation to get a deeper-nested value when used for component parameters in a CMS object.
- Added `auth.throttle.*` configuration options to configure the login throttling for the backend.
- Added `formGetRedirectUrl($context, $model)` method to the `FormController` behavior, overrideable by the implementing controller. Used to get the redirect URL for a given context & model if a redirect is requested.
- If uploaded files are missing an extension October will now try to automatically determine one based on the MIME type of the file.
- Added support for the `attributes` property on the `codeeditor` FormWidget.
- Added support for the `placeholder` attribute on the `password` field type.
- Added support for defining custom values for the `title` and `toolbarButtons` labels of the RelationController behavior.

## Bug Fixes
- Fixed an issue where data in a DataTable widget inside a relation model popup form would not be saved on submit.
- Record Finder widgets will now correctly save and load a record when using a column other than ID in the `keyFrom` configuration value, when the widget is not in relation mode.
- Fixed issue where custom validation rule strings starting with `unique` would not register correctly.
- Fixed `propertyExists()` method to correctly detect properties added through `addDynamicProperty()`.
- Fixed `options` support for `checkboxlist` and `balloon-selector` field types in the Syntax Parser
- Fixed issues with properly quoting values when running `october:env`
- Fixed issue where Excel wouldn't properly detect the encoding of CSV files exported using the `useList` option
- Changed optional .htaccess line forcing HTTPS to default to returning a 301 response instead of 302.

## Security Improvements
-

## Translation Improvements
- Improved German translation.
- Improved Russian translation.

## Performance Improvements
- Minor performance improvement by not calling Lang::get() every time a CMS Page object is instantiated.

## Community Improvements
-

## Dependencies
- Switched from the abandoned `jakub-onderka/php-parallel-lint` library to `php-parallel-lint/php-parallel-lint` for code linting purposes in the October CMS and Rain library test suites.
