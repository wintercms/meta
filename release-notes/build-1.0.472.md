# Build 1.0.472 (WIP)

> **NOTE:** As of v1.0.472, the core maintainer team has left October CMS and forked the project into Winter CMS.

## UX/UI Improvements
-

## API Changes
-

## Bug Fixes
-

## Security Improvements
- Tightened up the Twig SecurityPolicy. Calling `insert()`, `update()`, `delete()` methods on all PHP objects are now blocked from within Twig, data modifications should not be done at the view layer. If absolutely necessary, consider firing a view event instead. Backported from v1.1.2.
- Added a new config value (`app.trustedHosts`) to protect against [host header poisoning](https://portswigger.net/web-security/host-header). The following values can be used: the default of `true` will allow only the naked and `www` versions of `app.url` as trusted hosts, `false` will disable the feature (except on the backend password reset flow), and finally an array of trusted host patterns.
- Session identifiers are now invalidated on logging out instead of just flushed.

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-