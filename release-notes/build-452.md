# Build 452 (IN PROGRESS):

## UX/UI Improvements:
- Force values that would overflow a `.form-control` container to wrap to the next line instead of overflowing the field

## API Changes:
- Added `oc.inputPreset.beforeUpdate` JS event to the `input.preset.js` logic
- Added support for optional `$options` parameter to the `FormController`'s `formRenderField($name, $options)` method to be passed to the `Form` widget's `renderField($name, $options)` method.
- Added `role="form"` attribute to output of `Form::open()`

## Bug Fixes:
- Fixed issue with the `DataTable` FormWidget being unable to dynamically get dropdown options
- Fixed issue where `Form` widgets attached to the CMS backend controller would have a different alias on every request causing features that relied on consistent aliases to break (namely grouped repeaters in the CMS / RainLab.Pages section)
- Fixed issue where the `text` filter used a hardcoded widget alias instead of `getEventHandler()` 
- Fixed issue where when inserting an image with the `mediafinder` into a `richeditor` field, the image could sometimes be inserted at the top of the content instead of where the cursor was when it was originally selected
- Fix ability to clear `RecordFinder` fields when `useRelation` is set to `false`

## Security Improvements
-

## Translation Improvements:
- Improved Arabic translation
- Improved Hungarian translation

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-