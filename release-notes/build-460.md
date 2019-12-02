# Build 460 (WIP):

## UX/UI Improvements:
- Moved CodeEditor's full screen buttons to the bottom of the widget.
- Fixed keyboard support for checkboxes
- Added keyboard support to lists
- Improved the UX of checkbox lists "Select All", "Select None" bulk actions
- Changed the cursor to be a `grab` cursor when hovering over table headers to indicate that they are a scrollable container
- Made the record "Delete" button consistent across the core backend controllers by replacing User Roles & User Groups delete buttons with the standard trash can icon button
- Fixed issue where form tabs would initially be unstyled until the JS had loaded and initialized them
- Added support for making radio fields display inline by adding `cssClass: 'inline-options'` to their properties
- Added auto detection of the field `required` property for fields that have `required_if` model validation rules

## API Changes:
- Cookies are no longer serialized. This brings the behavior back in line with Laravel's default behavior as of the 5.5.42 update. **IMPORTANT**: If you are passing non-scalar values to `Cookie::set()` (i.e. objects & arrays) then you will need to change your code so that those values are JSON encoded / decoded before and after being stored in the cookie.
- Added new `System\Traits\ResponseMaker` trait to the base `Backend\Classes\Controller` class (and the `Cms\Classes\Controller` controller). Adds the following methods: `setStatusCode($code)`, `getStatusCode()`, `setResponse($response)`, `setResponseHeader($key, $values, $replace = true)`, `setResponseCookie($cookie)`, `getResponseHeaders()`, and `makeResponse($contents)`.
- `media.file.upload` event now passes the `$path` argument by reference.
- `media.file.upload` event now passes the `$path` argument by reference.
- Added ability to specify a LESS file to be used as a default backend brand CSS override with the config item `brand.customLessPath`
- Updated references to deprecated `event.which` and other methods of determining the selected keys to the new `event.key`
- Added new method `removePermission($owner, $code)` to the BackendAuth manager class to enable plugins to dynamically remove permissions from the available list registered with the BackendAuth manager class.
- Added support for SparkPost mail driver
- Added support for a string option to be provided to `October\Rain\Network\Http->setOption($option, $value)` as long as it corresponds to a valid `CURLOPT_` constant
- Added `getConfig($value, $default = null)` method to the `Backend\Classes\ListColumn` class to mirror what's available on the `Backend\Classes\FormField` class
- Added `order` option to the `relation` FormWidget to allow relation options to be ordered by a custom order statement.
- Added `email` field type (`type: email`)
- Documented newly available `services.mailgun.endpoint` config item in `config/services.php`
- Replaced existing handling of disabling CloudFlare's rocket loader on backend scripts by adding a new event (`system.assets.beforeAddAsset`) that is listened to by the `HeathDutton.CloudFlare` plugin. Recommend any CloudFlare users using Rocket Loader to use that plugin going forward
- Added support for `permissions` property on form fields, list columns, and list filter scopes. Property supports either a single string or an array of permissions that the current backend user must have access to at least one of in order to access the field / column / filter scope.
- Added support for `mode: switch` to the `Backend\FormWidgets\PermissionEditor` FormWidget that defines permissions as either expliclity allowed (1) or denied (-1).
- Added support for `availablePermissions` property to the `Backend\FormWidgets\PermissionEditor` FormWidget that accepts an array of permission codes to filter the list of permission codes to be managed by that widget instance down to.
- Added `clear-full`, `clear-left`, and `clear-right` CSS classes that can be used to apply clearfixes to form fields by adding them to the field's `cssClass` property
- Added support for the `CURLOPT_POSTFIELDS` cURL option to be manually overriden when using the `October\Rain\Network\Http` wrapper.
- Added support for `dependsOn` to filter scopes of `type: group`. All current filter scopes (including their current values) will be passed to the options method as an array of scope objects to be used in redetermining the available options to provide when the scopes that are targeted with `dependsOn` are updated.
- Added support for unregistered translation strings to still have the replacement engine run on them
- Added support for minimum or maximum values in number range filter to be left unspecified - this is treated as an "at least" minimum value or "at most" maximum value filter.
- If a List widget column is sorted, this sorting is applied exclusively, allowing users to sort records even if ordering is applied externally - for example, as a default order in a relation.

## Bug Fixes:
- Reverted improvements to table column width handling on Chrome (specifically for long unbroken text values in columns) introduced in Build 444 as it was causing other issues on mobile.
- Reduced inconsistencies with results generated by `\October\Rain\Database\Attach\Resizer` class, specifically for .gif images by processing .gif images with `imagescale()` instead of `imagecopyresampled()`
- Fixed an issue where attempting to modify the available Settings Items through the `SettingsManager` could fail if a user wasn't provided to `filterItemPermissions()` at that point in the request
- Removed caching of Theme configuration, this is now handled by `YAML::parseFile()` caching which simplifies the Theme processing code and fixes some bugs related to cache invalidation
- Fixed issue with trying to create multiple CMS templates at once
- Fixed issue where the cached classes file would not be removed along with the cached services file when running `php artisan clear-compiled`
- Fixed issue with PHP 7.0 compatibility introduced with new `PreferenceMaker` trait in Build 457
- Fixed issue where message subjects set in Mail callback functions were not available to the system mail layouts because the layouts were generated before the callback was called. Note that this was accomplished by calling the callback before content is added to the message instead of after, so it could be considered a breaking change
- Fixed styling for switch fields that are required
- Fixed bug where '0' was returned as NULL from `$this->param()` but returned as `'0'` from `{{ this.param.slug }}`
- Fixed issue where updating a record through a RelationController would not trigger a change event on the RelationController field like creating a record would by triggering the change event on successful update
- Fixed issue where FormWidgets in Repeaters that made orphaned AJAX requests (AJAX requests fired on an element outside of the repeater's markup structure, ex. from a popup modal instead) were not being initialized which was causing the orphaned requests to fail
- Fixed issue where the `databaseTemplates` feature from Build 456 wouldn't support templates in subfolders. Nesting limit is still 2 (`/template-type/subfolder1/template.htm`) but the issue where it was just 1 when `databaseTemplates` was enabled has been fixed.
- Fixed issue where the `change` event was not triggered on removing a recordfinder's value with the clear button
- Improved default email branding styles compatibility with Outlook mail clients by preventing harsh word breaks.
- Fixed issue where the Model class would try to trim an attribute that was a PHP resource (pgsql:bytea) by simplifying the trim detection logic to just use `is_string` instead of checking if value wasn't every other type of variable available.
- Fixed issue where an infinite loop could occur when trying to resolve a circular required_with or required_if validation rule chain.
- Fixed issue where having no class lists configured for the RichEditor markup class options would break the RichEditor.
- Fixed issue where the `model.beforeSave` event would be fired twice under some conditions when using a HasOneOrMany relationship.
- Fixed PHP fatal error under some cases where `argv` is not available in the server variables.
- Fixed issue where the FileUpload FormWidget was checking if the file model was protected before generating the URL to the file even though the File model itself handles that operation since Build 447.
- Fixed issue where the mediafinder formwidget wouldn't work when the user didn't have access to the Media Manager by switching the formwidget to preview mode under those conditions
- Fixed issue where text in an error message popup could not be selected for copy-pasting.
- Fixed issue with parsing the select2 options format over AJAX requests introduced in Build 457.
- Fixed conflict between input.trigger.js & filter.js that caused filter popup buttons to disappear when searching for records in a group filter popup.
- Fixed faulty type cast for belongsToMany deferring bindings table when using PostgreSQL
- Fixed support for mobile devices (touch screens) in the jquery.sortable.js plugin
- Fixed issue introduced in Build 459 where some server configurations could cause the AssetCombiner to stop working
- Fixed issue with number range filter not working with a value of `0` for either the minimum or maximum value.
- Fixed issue where attempting to sort by a column that isn't actually supported as a sortable column by the database could cause the session to enter an invalid state where it would be impossible to remove that column sorting preference.
- Fixed issue where changing just the "time" field on a `datepicker` FormWidget wouldn't trigger the JS `change` event on the field

## Security Improvements
- Prevent tabnabbing that could theoretically occur from a backend user clicking the "Preview" button in the backend navigation and having the tab taken over by the frontend site
- Added new global JS function `ocJSON()` to framework.js for parsing loose JSON safely

## Translation Improvements:
- Improved Polish translation
- Improved Chinese translation
- Improved French translation
- Improved Dutch translation
- Improved Portuguese translation
- Improved Hungarian translation
- Improved Russian translation
- Improved Czech translation
- Improved Slovak translation
- Added a translation key for the Repeater's "Add new item" text (`backend::lang.repeater.add_new_item`)

## Performance Improvements:
- Very minor performance improvement calling `JSON.parse()` instead of `$.parseJSON()` in core JS
- Added support for lazy loading the backend navigation menu icons / images
- Added caching of `YAML::parseFile()` when debug mode is disabled. The cache key is prefixed with `yaml::` and is generated from the path provided along with the last modified time of that file to ensure that it's always properly invalidated. Cache is stored for a maximum of 30 days.
- In instances where there is only one theme present and its code matches the code set in cms.activeTheme the database will no longer be asked what the currently active theme is, it will just be assumed that the only one present is the active theme.

## Community Improvements:
- Switched to using GitHub actions instead of Travis for CI on the main octobercms/october and octobercms/library repositories
- Added GitHub action to auto archive issues / pull requests after a month of inactivity
- Added initial frontend testing suite under `tests/js`
- Added API docs for `backend.page.beforeDisplay`, `backend.menu.extendItems`, `backend.user.login`, `backend.beforeRoute`, `backend.route`, `cms.beforeRoute`, `cms.route`, `cms.block.render`, `cms.combiner.beforePrepare`, `system.settings.extendItems`, and `system.extendConfigFile`

## Dependencies
- Updated Dropzone from v4.0.1 to v5.5.1
- Updated jQuery.Mousewheel from v3.1.9 to v3.2.0
- Updated Mustache from v2.0.0 to v2.3.2
