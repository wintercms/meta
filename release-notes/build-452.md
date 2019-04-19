# Build 452 (IN PROGRESS):

## UX/UI Improvements:
- Force values that would overflow a `.form-control` container to wrap to the next line instead of overflowing the field

## API Changes:
- Added `oc.inputPreset.beforeUpdate` JS event to the `input.preset.js` logic
- Added support for optional `$options` parameter to the `FormController`'s `formRenderField($name, $options)` method to be passed to the `Form` widget's `renderField($name, $options)` method.
- Added `role="form"` attribute to output of `Form::open()`
- Added automatic conversion of array notation to dot notation in validation rules (`attribute[nested]` to `attribute.nested`, etc)
- Added `cache` attribute to attributes supported by `addJs($script, $attributes)` to enable disabling the CloudFlare RocketLoader which causes issues in the backend.
- Simplified how the `Repeater` FormWidget works internally which should resolve some sporadic issues.
- Now using an embedded `Form` widget to process `FileUpload` file properties (like `title` and `description`). This enables dynamic extension of this form.
- Added automatic mimetype detection of `.svg` files as `image/svg+xml`

## Bug Fixes:
- Fixed issue with the `DataTable` FormWidget being unable to dynamically get dropdown options
- Fixed issue where `Form` widgets attached to the CMS backend controller would have a different alias on every request causing features that relied on consistent aliases to break (namely grouped repeaters in the CMS / RainLab.Pages section)
- Fixed issue where the `text` filter used a hardcoded widget alias instead of `getEventHandler()` 
- Fixed issue where when inserting an image with the `mediafinder` into a `richeditor` field, the image could sometimes be inserted at the top of the content instead of where the cursor was when it was originally selected
- Fix ability to clear `RecordFinder` fields when `useRelation` is set to `false`
- Fixed issues introduced in Build #449 with regards to the "Image not found" message showing up at incorrect times for the `MediaFinder` formwidget
- Fixed a bug where `track-input` triggered requests could return incorrect results by waiting until input is finished to fire requests triggered by tracking input

## Security Improvements
-

## Translation Improvements:
- Improved Arabic translation
- Improved Hungarian translation

## Performance Improvements:
- Added preloading of all essential scripts in the backend to improve performance
- Improved performance when utilizing remote storage drivers by caching the results of `hasFile()`.
- Cached the parsed theme configuration to improve performance on subsequent page loads

## Community Improvements:
-

## Dependencies
- Updated jQuery from V3.3.1 to V3.4.0