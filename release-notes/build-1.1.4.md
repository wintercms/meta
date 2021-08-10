# Build 1.1.4 (WIP)

## UX/UI Improvements
- Fixed visual issue with checkboxes in inspector popups where they would take up space but not be visible.
- The order of columns in the Lists widget will be reset when pressing the "Reset to Default" button in the List config popup.
- The password restore and reset pages in the Auth controller now provide a body class (`restore` and `reset`, respectively) for targeting CSS.

## API Changes
- `SystemException`s are now thrown for code paths resulting in not found exceptions (AJAX handlers, partials, content, components, etc) to make it easier to identify and resolve issues before end users are affected.
- Added the `getNamespaceAliases($namespace)` & `getReverseAlias($class)` methods to the `ClassLoader` class.
- Added `Winter\Storm\Support\Testing\MocksClassLoader` trait for mocking the ClassLoader in unit tests.
- The `Http` helper in the Storm library now stores and makes available all response headers in the `$headers` property even if the `toFile()` method is used - previously, headers would be discarded to prevent them being added to the file content.
- Custom Twig filters & functions registered in plugins via `registerMarkupTags()` can now specify the options to be used when registering the filters / functions with Twig.
- Added support for [Trusted Proxies](https://laravel.com/docs/6.x/requests#configuring-trusted-proxies) in Winter CMS, allowing sites behind proxies to still be served under HTTPS even if the HTTPS connection terminates at the proxy. Previously, the Backend of Winter CMS would redirect the user to the real underlying web address, which may not exist if it is proxied.
- Added support for providing a default image to be used for `type: image` backend list columns.

## Bug Fixes
- Fixed issue where warnings about removing replaced plugins were still shown even when the plugins had already been removed.
- Fixed support for multiple where clauses on the `unique` model attribute validation rule.
- Fixed support for uppercase file extensions when using the `ImageResizer` (i.e. `.JPG`, etc)
- Fixed a few issues with the `unique` validation rule (couldn't specify multiple where conditions, minor inconsitencies in how it was being parsed, etc) and added unit tests to cover all valid variations fo the rule
- Fixed issue where calling `url()` or `temporaryUrl()` on a filesystem driver that didn't support those methods would throw a `Class not found` exception instead the appropriate `RuntimeException`.
- Backported a fix from Laravel 7 to allow pagination for queries with `having` clauses.
- Fixed issue with NavigationManager items that had invalid `order` values causing the backend to crash.
- Fixed issue where requests to non-existant Asset Combiner routes would return a 500 error code instead of 404.
- Fixed issue where the replacing plugin would be disabled on the first request after an aliased plugin was disabled.
- Fixed issue where namespace aliases registered via the `ClassLoader` (usually through the plugin replacement functionality) would not be evaluated by the `Extendable` trait (i.e. behaviors were not resolving correctly).
- Fixed issue where `0` couldn't be used as the `min` or `max` value for `number` field types.
- Fixed an issue with SSL connection failures and the `winter:version` command on Mac OS by using the `Http` helper as opposed to the `file_get_contents()` method.

## Security Improvements
-

## Translation Improvements
- Improved French translation.
- Improved Latvian translation.
- Improved Italian translation.
- Improved Romanian translation.
- Improved Russian translation.
- Improved German translation.

## Performance Improvements
- Improved speeds with path resolution for Halcyon File datasources sharing the same base directory.

## Community Improvements
- Dropped old "build" files in the Storm library that were previously used for subsplitting the modules in the main Winter CMS repository for Composer. This has been replaced by a command in the Winter CMS CLI utility.
- Changed the default database host config option to be `127.0.0.1` instead of `localhost`. `localhost` may be slightly faster in some environments, but `127.0.0.1` is more reliable in all environments and the default can always be changed for specific projects that require it.
- Added automatic regeneration of the docs on [wintercms.com/docs](https://wintercms.com/docs) whenever a commit is made to the [docs repository](https://github.com/wintercms/docs) meaning that the public docs will finally be always up to date with the underlying git repository that powers them! Huge thanks to Marc Jauvin for finally taking care of a long standing annoyance with the project documentation.
- Updated the default config files to more closely match Laravel 6's default configurations.
- Improved issue templates on the main Winter CMS repository

## Dependencies
-
