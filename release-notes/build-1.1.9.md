# Build 1.1.9 (WIP)

## UX/UI Improvements
-

## API Changes
-

## Bug Fixes
- Improved support for read-only filesystems by using the Storage facade to handle the disabled plugins cache file instead of directly interacting with the local disk.
- Fixed the System Status dashboard widget on read-only filesystems.
- Fixed issue where calling `Snowboard.request()` with the element parameter set to false or null would fail.
- Fixed issue where changes made to `$this->vars` in a Partial's PHP code section wouldn't be available in the Twig section.

## Security Improvements
-

## Translation Improvements
- Improved German translation

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-