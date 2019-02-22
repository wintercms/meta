# Build 448 (IN PROGRESS):

## UX/UI Improvements:
- Improved consistency of file size displayed in the `FileUpload` FormWidget between upload and page load actions
- Added `Inline (No icons)` navigation mode to the branding settings

## API Changes:
- Changed `filter.js` to fire AJAX requests on the filter control element instead of the closest `form` element
- Changed the `datepicker` FormWidget when in mode `date` to send a DateTime string with zeroed time (according to the `app.timezone` configuration) using the client's timezone. This is a change from the previous behaviour of sending the current time.
- Added ability to specify a `permissions` array when registering `ReportWidgets` to force the user to have at least one of the specified permissions to be able to utilize the `ReportWidget` in question.
- Added support for `counter` and `counterLabel` to main menu items, `counter` will default to the sum of the relevant side menu `counter`s unless `counter` is set to false.
- Added support for multi-line update messages in plugin's `version.yaml` file
- Now firing the `backend.list.extendRecords` event from the `export()` method when `useList: true` in the `ImportExportController` behavior.
- `abort(404)` now returns the backend 404 view when called in the backend (module and plugin backend controllers)
- Added `plugin:list`, `plugin:disable Author.Plugin`, `plugin:enable Author.Plugin` Artisan CLI commands

## Bug Fixes:
- Fixed field default values when adding new items with the `Repeater` or when using `minItems` over 0
- Fixed support for nested jsonable properties as list columns (i.e. `additional_data[level_1][level_2]`)
- Fixed support for `DataTable` FormWidgets within Repeaters
- Fixed an issue where SVG menu icons wouldn't display on page load and required a repaint to actually display
- Fixed issue where the password in invitation emails was getting HTML encoded leading `123&test` to become `123&amp;test`
- Fixed issue with AJAX handlers in `ReportWidget`s, specifically related to issues with the widget aliases not being set correctly
- Fixed issue with being unable to use the second datepicker field's popup for a daterange filter inside of a popup
- Fixed issue with multibyte slugs, reduced default max length from 240 to 175 to account for the default DB charset of `utf8mb4`
- Fixed the `hasMany` relationship when not using the model's primary key as the the relationship's key
- Fixed issue where attempting to install plugins from the `october:install` CLI command wouldn't work due to plugins attempting to install themselves before October itself was configured.

## Security Improvements
-

## Translation Improvements:
- Improved Hungarian translation
- Improved Turkish translation
- Improved French translation

## Performance Improvements:
- Refactored `stripe-loading-indicator` to use CSS transforms instead of animating the `width` property to improve rendering performance.

## Community Improvements:
-

## Dependencies
-