# Build 453 (IN PROGRESS):

## UX/UI Improvements:
-

## API Changes:
-

## Bug Fixes:
- Truncate URLs in the Request Log to 191 characters instead of 255 to reflect the default DB schema of utf8mb4
- Fixed issue introduced in Build 452 where all themes would have their configuration cached under the same key causing issues when switching themes.
- Improve tab usability on mobile by disabling the swipe-to-change-tabs feature as it conflicted with tabs that had horizontal scrollable content.

## Security Improvements
- Escape more user provided inputs in the backend to minimize potential XSS

## Translation Improvements:
- Improved Viatnamese & Serbian input preset character mapping

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-