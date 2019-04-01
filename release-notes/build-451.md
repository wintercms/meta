# Build 451:

## UX/UI Improvements:
- Added support for `previewMode` to the `markdown` FormWidget

## API Changes:
- Added new configuration option `database.useConfigForTesting` to change the default behaviour of using the in-memory Sqlite DB driver for running automated tests to using whatever connection is defined by your configuration.
- Added `defaultFormatOptions` to the `ImportExportBehavior` to override the default format options to be used when exporting

## Bug Fixes:
- Fixed support for migration files in subdirectories
- Fixed `colorpicker` FormWidgets being unable to be manually updated while inside of a popup modal
- Fixed issue with getting request input from `get()` and `post()` that were introduced in Build 450.
- Fixed issue where grouped repeaters stopped working in Build 449

## Translation Improvements:
- Improved Russian translation