# Build 1.2.12

## UX/UI Improvements
- Added support for `tel` form field.

## Bug Fixes
- Fixed z-index on MediaManager move dropdown.
- Fixed support for config properties on URL fields.
- Fixed issue where dynamically extending a class to add behaviors could fail if the behavior had been added before.

## Security Improvements
- Added protection against privilege escalation attack from authenticated backend users.

## Performance Improvements
- Moved Vite rendering to `{% styles %}` Twig tag instead of `{% scripts %}` to prevent FOUC.

## Dependencies
- Improved support for PHP 8.4.
