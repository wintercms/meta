# Build 1.2.10

## UX/UI Improvements
- Replaced the codeeditor's implementation from Ace Editor to Monaco.
- Improved grouped repeater UX by adding search and multiple columns.
- Removed the `.` from the end of the generated password in the output of the `winter:passwd` command to make it easier to copy.

## DX Improvements
- Fixed support for the Laravel Maintenance mode (`artisan down`, `artisan up`) which was broken with the move to Laravel 9 (note: this is separate from the backend / CMS "soft" maintenance mode).
- Added support for the `schedule:list` and `schedule:work` commands from Laravel
- AutoDatasource caching is now disabled when `app.debug` is true to avoid issues caused by stale path caches when developing locally.
- Added `llms.txt` and `.user.ini` to the list of mirrored files.
- Made the dropdown field use the `Form::select()` helper internally for consistency.
- Made the repeater's `titleFrom` property less picky about what type of field it can pull the value from.

## API Changes
- Add support for images / icons in options with the `Form::select()` helper.

## Bug Fixes
- Fixed issue where emptyOption wasn't being removed in the `Form::select()` helper after being used to populate the placeholder.
- Fixed issue where the FontAwesome assets downloaded by the `winter:util compile less` command weren't being pinned to a specific version.
- Fixed issue where fancy layout form styles were bleeding into modals.
- Fixed issue where the loading indicator wouldn't hide after receiving a RedirectResponse for file downloads through the AJAX framework.

## Security Improvements
- Sanitize SVG files when uploaded to the theme assets.
- Improved escaping of EditorSettings, BrandSettings, & MailBrandSettings.

## Translation Improvements
- Improved Ukrainian translation.

## Community Improvements
- [OFFLINE.Mall](https://github.com/OFFLINE-GmbH/oc-mall-plugin) has been forked as a first-party plugin ([Winter.Mall](https://github.com/wintercms/wn-mall-plugin)).
- Added mail driver that adds support for the MS Graph API mailer ([Winter.DriverMSGraph](https://github.com/wintercms/wn-drivermsgraph-plugin)).
- Improved support for external SSO provider driver plugins in the [Winter.SSO](https://github.com/wintercms/wn-sso-plugin) plugin.
- Added [Winter.SSOProviderMicrosoft](https://github.com/wintercms/wn-ssoprovidermicrosoft-plugin) - Microsoft 365 and Azure AD authentication provider for [Winter.SSO](https://github.com/wintercms/wn-sso-plugin).
