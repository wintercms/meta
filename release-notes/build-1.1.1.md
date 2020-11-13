# Build 1.1.1

## UX/UI Improvements
- Adjusted `october:fresh` to remove the demo plugin even when the demo theme has already been removed.
- Allowed for the "fancy" breadcrumb widget to be styled based on custom branding colors specified in the "Customize back-end" settings.
- System will now throw an exception with a helpful error message if image resizing fails because an unsupported cache driver is being used (i.e. `array`).
- Switched the order of the "Install plugins" & "Install themes" buttons to match the order of the tabs on the actual install page
- Plugins that are already present in the local system and also exist in the marketplace will no longer be re-downloaded when a Project ID is attached.
- The plugin management page will now reload after making changes that would affect which plugins are currently active.

## API Changes
- The `october:env` command is now privileged and will run even if plugins are failing to boot.
- A new syntax for specifying the available options for field types that use the `options` property is now available: `\Path\To\Class::staticMethodName` will use the array returned by calling the static method `\Path\To\Class::staticMethodName()` as the options
- The `noRecordsMessage` configuration value to specify a message when a list is empty can now be specified for list-type widgets in the Relation controller.
- CMS pages that are hidden (only accessible to logged in backend users) will now be automatically removed from RainLab.Pages menus.
- `session.same_site` now defaults to `Lax` instead of null and any invalid configurations will be automatically corrected to the default value of `Lax`. See [#5293](https://github.com/octobercms/october/pull/5293) for a detailed breakdown.
- Added new `removeSideMenuItems()` helper method to `NavigationManager`, which can quickly remove one or more side menu items for a specific owner and menu.
- The app locale at the time of a message's entry onto the queue is now stored with the message on the queue as `_current_locale`.
- Added support for `$query->selectConcat(array $parts, string $as)` to concatenate an array of parts into a single column/attribute `$as`.
- Added support for the `upsert($values, $uniqueBy, $updateColumns)` QueryBuilder method added in Laravel 8.x which allows for bulk updates or inserts at the database level.
- Added separate `backend.manage_own_editor` permission to allow users to manage their own personal editor preferences without being able to modify the global ones.
- Added new `media_path()` helper function to return the fully qualified path to the media directory.
- Added new `Storage::identify($disk)` method to identify the name of the disk configuration used to instantiate the given disk instance.
- Template blocks in Backend templates are now correctly terminating the output buffering used. Block processing uses layers of output buffering to determine applicable block content, however, a particular scenario occurred where subsequent blocks were not rendered due to content in between two blocks cancelling another layer, causing issues with further blocks. The block functionality will now capture the content in between blocks and hold it until the final content is generated, keeping the correct layer intact so that subsequent blocks are kept in the right location. See https://github.com/octobercms/library/pull/517 for more information.
- Added new `October\Rain\Database\Behaviors\Sortable` behavior that mirrors the functionality of the `October\Rain\Database\Traits\Sortable` trait except with the ability to dynamically attach it to models at runtime allowing for third-party plugins to be extended with the functionality.
- Themes can now register localization keys to be used only on the backend using a similar file structure to plugins & modules. Ex: `themes/mytheme/lang/en/lang.php` contains `'ga_api_key' => 'Google Analytics API Key'`, referenced by `themes.mytheme::lang.ga_api_key`.

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
- Fixed a long-standing issue where returning a redirect to a file in response to an AJAX request in order to get the browser to download the file wouldn't stop displaying the AJAX loading indicator.
- Fixed the `uploads_path()` helper.
- Fixed support for AWS S3 as a source for the ImageResizer.
- Fixed issue where backend administrators list could not be filtered by "Is superuser?" filter on SQL Server due to that database engine not supporting literal boolean values.
- Fixed adjacent block placeholders not working in Backend templates - the initial block is rendered, but the subsequent block is ignored. See API change above regarding block termination for more information.

## Security Improvements
- Tightened up the default permissions granted to the "Publisher" system role out of the box
- Improved handling of custom editor styles to prevent HTML injection
- Locked down the Twig sandbox even more to prevent allowing users with access to Twig templates from defining and running PHP code

## Translation Improvements
- Improved Taiwanese translation
- Improved French translation
- Improved Slovenian translation
- Improved Russian translation
- Improved Italian translation
- Improved Dutch translation
- Improved German translation

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
