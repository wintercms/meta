# Build 442:

## UX/UI Improvements:
- Improved Repeater styling by styling items as individual "panels" and added an index tracker to the side of each item
- Added support for displaying the required indicator next to form fields that are marked as required with nested validation: `property.*.subfield`
- Automatically use field labels as custom attribute names in validation messages thrown by the Form widget

## API Changes:
- Added `inline-options` property to `checkboxlist` field type to display checkboxes inline
- Added `fromUrl()` method to the `File` model for creating a file from a provided URL

## Bug Fixes:
- Fixed critical bug with deferred binding when using PostgreSQL