# Build 1.2.3

## UX/UI Improvements
- Display an inspirational quote after generating code files with the `create:*` scaffolding commands, can be disabled by passing the `--uninspiring` option.
- `InvalidArgumentException` exceptions in scaffolding commands are now caught and displayed as an error in the console.
- Support for uploading SVGs is now present and enabled by default in the core. SVGs are sanitized on upload to avoid potential XSS attacks.
- Minor improvements to the backend brand settings page on mobile.
- Added a visual indicator to ignored packages when running `artisan mix:list`.
- Added ability to select the desired theme scaffold to use when scaffolding themes from the backend, also will now automatically pre-fill more fields.
- Migration messages will now be show when running migrations in the console, even if an exception is thrown.
- Finished implementing the `artisan create:migration` command, with support for the `--version`, `--create`, `--update`, `--table`, and `--model` options. This command supports generating the required versions in `updates/version.yaml` now as well.
- A default `.env.example` file is now included in the `wintercms/winter` repository.
- Fixed an issue where the `Clear` button on the `recordfinder` wasn't visible.

## API Changes
- Local extensions are now initialized after all behaviours have been loaded. See [wintercms/storm@004159](https://github.com/wintercms/storm/commit/a8ba4eef2e96851c5f2293f1fbf70047c3004159).
- Ignored Mix packages are now excluded from `MixAssets::getPackages()` unless the `$includeIgnored` argument is true.
- Added `getPluginVersions()` method to the `PluginBase` class to get a sorted list of the plugin's versions as defined in `updates/version.yaml`.
- `cms.beforeRoute` is now a halting event in order to enable preventing the CMS catch-all route from being registered.

## Bug Fixes
- When updating the sort_order on sortable relations, `find()` is now called on the related model directly rather than the Relation object. See [wintercms/storm#146](https://github.com/wintercms/storm/commit/94a426f76dff251b8c10639490415806f034ee1a).
- Fixed issue preventing users from being able to create themes from the backend (Return value must be of type string, null returned).
- Fixed issue with case sensitivity when determining "upload_max_filesize" size.
- Fixed race condition with maxItem limit check after adding a new repeater item
- Fixed issue where keyboards could appear on mobile when attempting to use a datepicker field.
- Fixed issue where an error message was being logged unnecessarily.
- Fixed issue where dynamically switching between multiple themes on the same instance coud result in assets from the wrong theme being loaded.

## Security Improvements
- SVGs are now sanitized on upload to avoid potential XSS attacks. See [wintercms/winter#GHSA-wjw2-4j7j-6gc3](https://github.com/wintercms/winter/security/advisories/GHSA-wjw2-4j7j-6gc3).

## Translation Improvements
- Improved Hungarian translation.

## Performance Improvements
-

## Community Improvements
- The [Winter.Blocks](https://github.com/wintercms/wn-blocks-plugin) plugin has been released, offering a visual, block-based content editor for Winter CMS.
- The [Winter.Ray](https://github.com/wintercms/wn-ray-plugin) plugin now supports loading the Ray configuration through the normal Winter CMS config system rather than requiring a `ray.php` file to be present in your project root.

## Dependencies
- `winter/storm` and `wintercms/winter` now include PHP 8.2 in their automated test suites.
- Support for `symfony/console` up to `6.3` has been added.
