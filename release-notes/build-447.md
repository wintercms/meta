# Build 447:

## UX/UI Improvements:
-

## API Changes:
- Renamed the Lists widget's `prepareModel()` method to `prepareQuery()` instead.

## Bug Fixes:
- Fixed issue when the user's current page number for the list widget no longer existed (for any number of reasons) causing them to become stuck on a non-existent page. Fixed by using the last available page number in that case.
- Fixed Filter options being escaped twice (once by Mustache, once by the internal options retrieval logic)
- Fixed being unable to detect the Enter and Backspace / Delete keys in the `keydown.oc.richeditor` event by attaching the event before internal Froala capturing events are run.
- Fix the input trigger API where the form element doesn't exist

## Security Improvements
-

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