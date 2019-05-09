# Build 455 (WIP):

## UX/UI Improvements:
- Implemented easy impersonation of backend users through the backend - feature controlled by the new `backend.impersonate_users` permission

## API Changes:
- Changed the FileUpload FormWidget to process uploads with a `onUpload` AJAX handler instead of the `checkUploadPostback` method
- Changed the default value of `cache.disableRequestCache` to be `null` which now disables the in memory request cache during CLI requests and enables it during HTTP requests. Other values are explicit `true` or `false`.

## Bug Fixes:
-

## Security Improvements
-

## Translation Improvements:
- Improved Dutch translation

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-