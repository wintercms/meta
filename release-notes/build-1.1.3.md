# Build 1.1.3 (WIP)

## UX/UI Improvements
-

## API Changes
- Added support for modifying the RichEditor's allowed attributes list through the EditorSettings in the backend

## Bug Fixes
- Fixed issue with Schedule->withoutOverlapping() by bringing the Halcyon MemoryRepository more inline with the parent class.
- Fixed an error thrown when using the "package:discover" command when `app.loadDiscoveredPackages` set to false, as the manifest was reset to `null` as opposed to an empty array.
- Fixed issue where tooltips set on the first column of the Lists widget were not working.

## Security Improvements
-

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
- Documented the Lists widget's `perPageOptions` configuration property

## Dependencies
-
