# Build 1.1.4 (WIP)

## UX/UI Improvements
- Fixed visual issue with checkboxes in inspector popups where they would take up space but not be visible.

## API Changes
-

## Bug Fixes
- Fixed issue where warnings about removing replaced plugins were still shown even when the plugins had already been removed.
- Fixed support for multiple where clauses on the `unique` model attribute validation rule.
- Fixed support for uppercase file extensions when using the `ImageResizer` (i.e. `.JPG`, etc)
- Fixed a few issues with the `unique` validation rule (couldn't specify multiple where conditions, minor inconsitencies in how it was being parsed, etc) and added unit tests to cover all valid variations fo the rule
- Fixed issue where calling `url()` or `temporaryUrl()` on a filesystem driver that didn't support those methods would throw a `Class not found` exception instead the appropriate `RuntimeException`.
- Backported a fix from Laravel 7 to allow pagination for queries with `having` clauses.

## Security Improvements
-

## Translation Improvements
- Improved French translation.
- Improved Latvian translation.
- Improved Italian translation.
- Improved Romanian translation.
- Improved Russian translation.

## Performance Improvements
-

## Community Improvements
- Dropped old "build" files in the Storm library that were previously used for subsplitting the modules in the main Winter CMS repository for Composer. This has been replaced by a command in the Winter CMS CLI utility.
- Changed the default database host config option to be `127.0.0.1` instead of `localhost`. `localhost` may be slightly faster in some environments, but `127.0.0.1` is more reliable in all environments and the default can always be changed for specific projects that require it.
- Added automatic regeneration of the docs on [wintercms.com/docs](https://wintercms.com/docs) whenever a commit is made to the [docs repository](https://github.com/wintercms/docs) meaning that the public docs will finally be always up to date with the underlying git repository that powers them! Huge thanks to Marc Jauvin for finally taking care of a long standing annoyance with the project documentation.
- Updated the default config files to more closely match Laravel 6's default configurations.

## Dependencies
-
