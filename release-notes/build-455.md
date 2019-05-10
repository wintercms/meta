# Build 455 (WIP):

## UX/UI Improvements:
- Implemented easy impersonation of backend users through the backend - feature controlled by the new `backend.impersonate_users` permission

## API Changes:
- Changed the FileUpload FormWidget to process uploads with a `onUpload` AJAX handler instead of the `checkUploadPostback` method
- Changed the default value of `cache.disableRequestCache` to be `null` which now disables the in memory request cache during CLI requests and enables it during HTTP requests. Other values are explicit `true` or `false`.
- Brought the `AuthManager` and `User` classes more in line with Laravel's Auth library; full support is still a far ways off though.

## Bug Fixes:
- Fixed issue with retaining transparency when making thumbnails for some image files

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