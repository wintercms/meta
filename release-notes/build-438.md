# Build 438:

## UX/UI Improvements:
- Added ability to close tabs on middle mouse click
- Automatically reset list pagination to the first page when the filter is changed (which would change the results displayed)
- Added `align` support to non-sortable column headers
- Prevent showing the mail branding menu item to users without the permissions to actually use it
- Display an error if a migration file has been requested by a plugin but doesn't actually exist

## API Changes:
- Enabled use of unencrypted cookies with the `cookie.unencryptedCookies` configuration item
- Added `showWeekNumber` property to the `DatePicker` FormWidget
- Added support for minifying the core AJAX framework assets when debug mode is disabled
- Added `cms.restrictBaseDir` configuration item to allow local development to use symlinked files as if they were local to the application root.

## Bug Fixes:
- Removed circular dependency in the system LESS files
- Fixed issues with using tabs, repeaters, & the JS Trigger API together

## Translation Improvements:
- Added Slovak (SK) translation