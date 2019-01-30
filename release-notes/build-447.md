# Build 447:

## UX/UI Improvements:
- Added Backend 404 page, throw 404 instead of an exception on missing backend controller actions when debug mode is disabled.
- Added "Go to previous page" link to the Backend Access Denied page

## API Changes:
- Renamed the Lists widget's `prepareModel()` method to `prepareQuery()` instead.
- Provided the containing `Form` widget to `FormWidgetBases` instances as `$widget->getParentForm()` to enable complex FormWidgets to correctly obtain their containing `Form` widget instance.
- Implemented automatic backend URL generation for protected file's getPath() and getThumb() methods
- Added `returnResponse` parameter to `output()` and `outputThumb()` methods on the `October\Rain\Database\Attach\File` class to return `Response` objects instead of outputting the response headers and content directly.
- Added `validateUserModel()` method to the AuthManager class to provide an opportunity to reject a user's login
- Added `step`, `min`, & `max` options to the `number` field type.
- Added support for the `recordfinder` FormWidget to be used without a relationship definition through the `useRelation: false` and `modelClass` config properties
- Added support for the `brand.faviconPath` config option (and backend customization option) to load a custom favicon for the backend to use
- Added support for the `data-request-url` attribute to change the URL that the AJAX API fires an AJAX request to
- Added `getClassMethods()` method to the `ExtendableTrait` as a replacement for `get_class_methods()` to include the dynamic methods that are available within the class as well

## Bug Fixes:
- Fixed issue when the user's current page number for the list widget no longer existed (for any number of reasons) causing them to become stuck on a non-existent page. Fixed by using the last available page number in that case.
- Fixed Filter options being escaped twice (once by Mustache, once by the internal options retrieval logic)
- Fixed being unable to detect the Enter and Backspace / Delete keys in the `keydown.oc.richeditor` event by attaching the event before internal Froala capturing events are run.
- Fix the input trigger API where a `form` element doesn't exist
- Fixed returning false from `model.beforeValidate` not halting the validation process.
- Fixed FormWidgets not picking up the correct `previewMode` setting from their parent Form on AJAX requests that do not call the parent Form's `render()` method.
- Reduced reliance on the CMS module from the Backend module to improve stability of instances that just use the Backend and System modules (i.e. web applications)
- Only translate default values when they are strings (not arrays as in the case of default values for Repeaters).
- Fixed display of the "Clear search" button in various contexts
- Improved error messages in the YAML parser
- Fixed issue from Build 444 where tabs and tables were no longer horizontally scrollable on touch devices
- Fixed issue with simplePaginate using Laravel's translation system for Next & Previous which doesn't work in October
- Fixed insidious bug where HasOne relationship's `getSimpleValue` would return the key of the parent record, not of the actual related record.
- Fixed issue introduced in Build 446 where some media URLs would contain the base folder twice in a row
- Fixed issue with expanding / collapsing the side menu items within the backend settings section
- Fixed the `Repeater`'s "Add item" (grouped mode) popover in a popup context
- Fixed `dropdown`'s support for the `placeholder` attribute.

## Security Improvements
- Added escaping to more variables to prevent potential XSS attacks

## Translation Improvements:
-

## Performance Improvements:
-

## Community Improvements:
- Now running automatic CI tests with PHP 7.3

## Documentation Improvements:
- Added better documentation on how to register custom validation rules within plugins, credit to [Ben Thomson](https://github.com/bennothommo)

## Dependencies
-