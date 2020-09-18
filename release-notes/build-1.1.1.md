# Build 1.1.1

## UX/UI Improvements
- Adjusted `october:fresh` to remove the demo plugin even when the demo theme has already been removed.

## API Changes
- The `october:env` command is now privileged and will run even if plugins are failing to boot.
- A new syntax for specifying the available options for field types that use the `options` property is now available: `\Path\To\Class::staticMethodName` will use the array returned by calling the static method `\Path\To\Class::staticMethodName()` as the options

## Bug Fixes
- Fixed issue where displaying protected file thumbnails with a width or height set to nothing would fail.
- Fixed issue where URLs to resized images were not being properly URL encoded
- Fixed an issue introduced in Build 1.1.0 where plain Twig templates couldn't be loaded through the `{% include 'path' %}` or `{{ source(path) }}` Twig functions.
- Fixed issue introduced in build 1.0.458 where non-grouped repeaters with minimum items specified via the `minItems` option did not pre-fill the repeater with the minimum items.
- Fixed issue where the ImageResizer would attempt to process image types that it couldn't handle instead of just passing them through untouched.
- Fixed issue where resized images were not correctly identified as already having been resized when atomic (blue/green) deployment strategies are used in conjunction with files being stored on the local filesystem in a shared symlinked storage folder.

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
