# Build 1.1.7 (WIP)

## UX/UI Improvements
- You can now define one or more IP addresses that may view the site during maintenance mode via the Maintenance mode Settings screen.

## API Changes
- Added `$data` as the fourth argument to the `mailer.prepareSend` and `mailer.send` events.

## Bug Fixes
- Fixed issue introduced in v1.0.466 where copying the default RelationController markup to use in a controller-level override of RelationController partials would result in an "undefined index" exception.
- Client language files for child locales (i.e. `en-ca`) will now include fallback strings from their parent locales.

## Security Improvements
-

## Translation Improvements
- Improved Persian translation.
- Improved Latvian translation.
- Improved Russian translation.
- Improved German translation.

## Performance Improvements
-

## Community Improvements
- Winter CMS can now be accessed via the [Gitpod](https://gitpod.io) service, providing near-instant, fully working copies of Winter CMS for testing and development. Please see https://github.com/wintercms/winter/pull/295 for more information.

## Dependencies
-
