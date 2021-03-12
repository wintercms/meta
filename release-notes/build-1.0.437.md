# Build 1.0.437:

## API Changes:
- Added dot notation support to `extendClassWith()` method
- Added `attachOnUpload` property to the `FileUpload` FormWidget to attach the file directly to the parent record as soon as the upload completes instead of waiting for deferred binding to attach the file
- Added `cache.codeParserDataCacheKey` configuration item to prevent issues when running multiple Winter CMS instances attached to the same cache server

## Bug Fixes:
- Fixed infinite loop that could be triggered in the AuthManager
- Improved the SectionParser logic, fixing a bug with Markdown headers
- Improved PHP 7.2 support

## Security Improvements
- Prevent template files from being loaded outside of the application root
- Prevent invalid folders from being created in the Media Library

## Translation Improvements:
- Improved Polish translation
- Improved German translation