# Build 1.1.1

## UX/UI Improvements
- Adjusted `october:fresh` to remove the demo plugin even when the demo theme has already been removed.
- Allowed for the "fancy" breadcrumb widget to be styled based on custom branding colors specified in the "Customize back-end" settings.
- System will now throw an exception with a helpful error message if image resizing fails because an unsupported cache driver is being used (i.e. `array`).

## API Changes
- The `october:env` command is now privileged and will run even if plugins are failing to boot.
- A new syntax for specifying the available options for field types that use the `options` property is now available: `\Path\To\Class::staticMethodName` will use the array returned by calling the static method `\Path\To\Class::staticMethodName()` as the options
- The `noRecordsMessage` configuration value to specify a message when a list is empty can now be specified for list-type widgets in the Relation controller.
- CMS pages that are hidden (only accessible to logged in backend users) will now be automatically removed from RainLab.Pages menus.
- `session.same_site` now defaults to `Lax` instead of null and any invalid configurations will be automatically corrected to the default value of `Lax`. See [#5293](https://github.com/octobercms/october/pull/5293) for a detailed breakdown.
- Added new `removeSideMenuItems()` helper method to `NavigationManager`, which can quickly remove one or more side menu items for a specific owner and menu.
- The app locale at the time of a message's entry onto the queue is now stored with the message on the queue as `_current_locale`.
- Added support for `$query->selectConcat(array $parts, string $as)` to concatenate an array of parts into a single column/attribute `$as`.

## Bug Fixes
- Fixed issue where displaying protected file thumbnails with a width or height set to nothing would fail.
- Fixed issue where URLs to resized images were not being properly URL encoded
- Fixed an issue introduced in Build 1.1.0 where plain Twig templates couldn't be loaded through the `{% include 'path' %}` or `{{ source(path) }}` Twig functions.
- Fixed issue introduced in build 1.0.458 where non-grouped repeaters with minimum items specified via the `minItems` option did not pre-fill the repeater with the minimum items.
- Fixed issue where the ImageResizer would attempt to process image types that it couldn't handle instead of just passing them through untouched.
- Fixed issue where resized images were not correctly identified as already having been resized when atomic (blue/green) deployment strategies are used in conjunction with files being stored on the local filesystem in a shared symlinked storage folder.
- Fixed issue where the media manager would not display a folder that a contained a filename with characters that are considered invalid by the MediaLibrary class (i.e. '+', various unicode characters).
- Fixed issue where resized images with spaces in their filenames would not pass the resizer validation checks because the target URL would be decoded three times instead of the intended two.
- If a model's dateFormat includes microseconds (`.u`) or milliseconds (`.v`) but a given value provided to an attribute that is cast as a date does not include that information, then the date casting logic will now automatically add the appropriate number of zeros to the end of the provided date value for it to be accepted when parsing the provided value according to the defined dateFormat for the model. This fixes an issue with databases that have `.u` or `.v` in date columns that are managed by the datepicker in the backend which doesn't support sending micro or milliseconds.

## Security Improvements
- Tightened up the default permissions granted to the "Publisher" system role out of the box

## Translation Improvements
- Improved Taiwanese translation
- Improved French translation
- Improved Slovenian translation
- Improved Russian translation
- Improved Italian translation

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
