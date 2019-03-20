# Build 449 (IN PROGRESS):

## UX/UI Improvements:
- Redirect users with the `manage_theme_options` (but not the `manage_themes`) permission directly to the Customize theme page

## API Changes:
- Support `enableDefaults` on repeaters using grouped mode
- Simplified the `Repeater` item's data saving process by calling each item's `Form` widget's `getSaveData()` method instead of attempting to process the data directly.
- Disabled `FormWidget`s are now ignored in the `Form` widget's `getSaveData()` method just like regular form fields are.

## Bug Fixes:
- Fixed Save & Close button on the `ThemeOptions` update view
- Fixed long standing issue with being unable to update translated values with the RelationController
- Fixed issue where Repeaters with the same field names being bound to the same controller would cause confusing conflicts as they tried to process each other's data.
- Fixed issue where having the CMS module present but disabled would still try to handle backend 404's with the CMS controller.
- Fixed issue where multiple `Filter` widgets could not exist on the same page at the same time.

## Security Improvements
-

## Translation Improvements:
- Improved French translation

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-