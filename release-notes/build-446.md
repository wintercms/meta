# Build 446:

## API Changes:
- Added `format` property to `text` and `number` type columns which runs the value through `sprintf` using the provided `format`.
- Added new `nestedform` widget that allows you to infinetly nest forms inside of each other for maximum reusability of fields that are stored in model array attributes (such as `jsonable` or `encryptable`)
- Added `option` as an alias for `alt` in `input.hotkey.js` for Mac developers
- Pass the originating event object to the callback function in `input.hotkey.js` as the third parameter
- Added `backend.manage_default_dashboard` permission to lock down who has access to change the system's default dashboard configuration

## Bug Fixes:
- Fixed issue with the backend upgrade process to Build 444 where the user model would be retrieved before running the migration that added the `deleted_at` column to the users table
- Fixed support for the `placeholder` option on `richeditor` fields
- Fixed issue where using the clear search button in a Search widget that was within an HTML form element would cause the form to submit

## Translation Improvements:
- Minor improvements to Brazilian Portugese translation
- Improvements to Spanish translation

## Community Improvements:
- Updated the [OctoberCMS Contributing Guidelines](https://github.com/octobercms/october/blob/master/.github/CONTRIBUTING.md)
- Added issue & PR templates
- Moved Code of Conduct to it's own file