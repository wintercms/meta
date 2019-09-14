# Build 460 (WIP):

## UX/UI Improvements:
- Moved CodeEditor's full screen buttons to the bottom of the widget.
- Fixed keyboard support for checkboxes
- Added keyboard support to lists

## API Changes:
- `media.file.upload` event now passes the `$path` argument by reference.
- Added new global JS function `ocJSON()` to framework.js (also available in separate `framework.parser.js`) for parsing loose JSON safely

## Bug Fixes:
- Reverted improvements to table column width handling on Chrome (specifically for long unbroken text values in columns) introduced in Build 444 as it was causing other issues on mobile.

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
- Very minor performance improvement calling `JSON.parse()` instead of `$.parseJSON()` in core JS

## Community Improvements:
-

## Dependencies
- Updated Dropzone from v4.0.1 to v5.5.1
- Updated Modernizr from v3.6.0 to v3.7.1
- Updated jQuery.Mousewheel from v3.1.9 to v3.2.0
