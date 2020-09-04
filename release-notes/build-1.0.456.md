# Build 1.0.456:

## UX/UI Improvements:
- Added default "hard" (`artisan down`) maintenance mode view, able to be overridden by a `maintenance.php` file placed in the project root.
- Added support for previewing SVG images in the Media Library

## API Changes:
- Added `Url::buildUrl()` method (along with helper `http_build_url()`) as a polyfill for the PECL HTTP `http_build_url()` function.
- Added support for database-driven theme templates, enable `cms.databaseTemplates` to use it

## Bug Fixes:
- Fixed issues with hasMany relationship management by reverting some performance PRs to that process that were causing issues.
- Fixed adding new dashboard widgets defaulting to full screen width instead of 5/6th of full screen.