# Build 1.2.11

## UX/UI Improvements
- Added "Failed Logins" tab to the User account form in the backend to view the throttle records of users and be able to manually unthrottle IPs.
- Reorganized the fields on the user account page in the backend for ease of use.
- Added support for autogenerating passwords when creating users in the backend (requires notification email to be sent to the user).
- Added ability for the `CodeEditor` to restore its original line location when restoring after being disposed of on a page (i.e. when switching between on-page tabs with multiple codeeditors, like in the CMS Theme Editor).

## API Changes
- Added auto detection of `LICENCE` and `LICENSE` files in plugins as their license files.

## Bug Fixes
- Fixed bug introduced in v1.2.10 where collections weren't being supported as a possible value for form field's `options` property.
- Fixed bug introduced in v1.2.10 where `LESS`, `SASS`, and `SCSS` files were being treated as PHP files by the `CodeEditor` in the CMS Theme Editor.
- Fixed support for `type="module"` inline script tags when using the `Twig` language mode with the Monaco `CodeEditor`.
- Fixed bug introduced in v1.2.10 where event listeners attached to Theme events from within plugin `boot()` methods weren't being fired.

## Security Improvements
- Improved automatic sanitization of SVGs through the CMS `AssetList` widget.

## Community Improvements
- Fix PHP Code block examples for the `model.*` events in the Winter CMS documentation.
