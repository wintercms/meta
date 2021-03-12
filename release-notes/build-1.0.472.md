# Build 1.0.472

> **NOTE:** As of v1.0.472, the core maintainer team has left October CMS and forked the project into Winter CMS.

## UX / UI Improvements
- Fix support for browser-based validation of checkboxes and radio options

## API Changes:
- Added `registerOwnerAlias($owner, $alias)` to the `NavigationManager` to add aliases for given owners of registered menu items.
- Added `registerPermissionOwnerAlias($owner, $alias)` to the `AuthManager` to add aliases for given owners of registered permissions.
- Added `registerOwnerAlias($owner, $alias)` to the `SettingsManager` to add aliases for given owners of registered setting items.

## Security Improvements
- Tightened up the Twig SecurityPolicy. Calling `insert()`, `update()`, `delete()` methods on all PHP objects are now blocked from within Twig, data modifications should not be done at the view layer. If absolutely necessary, consider firing a view event instead. Backported from v1.1.2.
- Added a new config value (`app.trustedHosts`) to protect against [host header poisoning](https://portswigger.net/web-security/host-header). The following values can be used: `true` will allow only the naked and `www` versions of `app.url` as trusted hosts, the default of `false` will disable the feature (except on the backend password reset flow), and finally an array of trusted host patterns.
- Session identifiers are now invalidated on logging out instead of just flushed.