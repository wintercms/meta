# Build 466 (WIP)

## UX/UI Improvements
-

## API Changes
- Menu items controlled by `NavigationManager` are now objects, and `$manager->getMainMenuItem($owner, $code)` has been added to make it easier to manipulate existing menu items without having to deregister and reregister menu items to apply changes.

## Bug Fixes
-

## Security Improvements
-

## Translation Improvements
-

## Performance Improvements
- Minor performance improvement by not calling Lang::get() every time a CMS Page object is instantiated.

## Community Improvements
-

## Dependencies
-
