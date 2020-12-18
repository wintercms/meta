# Build 1.0.472 (WIP)

## UX/UI Improvements
-

## API Changes
-

## Bug Fixes
-

## Security Improvements
- Tightened up the Twig SecurityPolicy. Calling `insert()`, `update()`, `delete()` methods on all PHP objects are now blocked from within Twig, data modifications should not be done at the view layer. If absolutely necessary, consider firing a view event instead. Backported from v1.1.2.

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-