# Build 1.1.1

## UX/UI Improvements
-

## API Changes
- The `october:env` command is now privileged and will run even if plugins are failing to boot.
- A new syntax for specifying the available options for field types that use the `options` property is now available: `\Path\To\Class::staticMethodName` will use the array returned by calling the static method `\Path\To\Class::staticMethodName()` as the options

## Bug Fixes
- Fixed issue where displaying protected file thumbnails with a width or height set to nothing would fail.
- Fixed issue where URLs to resized images were not being properly URL encoded

## Security Improvements
- Tightened up the default permissions granted to the "Publisher" system role out of the box

## Translation Improvements
- Improved Taiwanese translations

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
