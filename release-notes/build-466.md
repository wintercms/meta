# Build 466 (WIP)

## UX/UI Improvements
-

## API Changes
- Menu items controlled by `NavigationManager` are now objects, and `$manager->getMainMenuItem($owner, $code)` has been added to make it easier to manipulate existing menu items without having to deregister and reregister menu items to apply changes.
- The `postbackHandler` property for DataTable form widgets now defaults to `null` - the widget will interpret a `null` value as to detect the save handler for the form that contains the widget (this is usually `onSave`, the old default value, but it will now detect other handlers such as those used by the relation controller).
- The `getParameter` method in `Cms\Classes\Router` is now correctly type-hinted.
- External parameters may now use dot notation to get a deeper-nested value when used for component parameters in a CMS object.

## Bug Fixes
- Fixed an issue where data in a DataTable widget inside a relation model popup form would not be saved on submit.
- Record Finder widgets will now correctly save and load a record when using a column other than ID in the `keyFrom` configuration value, when the widget is not in relation mode.

## Security Improvements
-

## Translation Improvements
- Improved German translations.

## Performance Improvements
- Minor performance improvement by not calling Lang::get() every time a CMS Page object is instantiated.

## Community Improvements
-

## Dependencies
-
