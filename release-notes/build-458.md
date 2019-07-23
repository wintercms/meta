# Build 458 (WIP):

## UX/UI Improvements:
- The link to "Access Logs" in the System Dashboard Widget is now hidden when the user doesn't have access to view those logs.

## API Changes:
- Added `cms.runMigrationsOnLogin` configuration item to control whether the UpdateManager automatically runs any pending migrations on login to the backend. The default is now `null` which means that the value is pulled from `app.debug`; i.e. only enabled when the application is in debug mode.

## Bug Fixes:
- Fixed support for tab icons in the Theme customization form
- Fixed support for default values in nestedforms inside of repeaters in an update context

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-