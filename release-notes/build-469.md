# Build 469 (WIP)

>**NOTE:** This build contains a number of changes made as a part of the upgrade from Laravel 5.5 LTS to 6.x LTS, it is highly recommended that you [review the upgrade guide](https://github.com/octoberrain/meta/blob/master/l6-upgrade-notes.md) to ensure you aren't affected.

## UX/UI Improvements
- Added new "sensitive" field widget that provides a revealable password field for forms.

## API Changes
- Added new development configuration option `develop.allowDeepSymlinks` which allows for symlinks at any subdirectory level when generating a public URL from a local path.
- The `System\Controllers\Settings` controller now provides a `formGetWidget` method to retrieve the form widget used for Settings forms.
- The default password validation rules for `Backend\Models\User` and `October\Rain\Auth\Models\User` have been loosened by no longer having a max length since passwords are stored in the database as hashed values and the length of the input has no effect on the length of the output.
- `october:env` will now use `QUEUE_CONNECTION` instead of `QUEUE_DRIVER` to refer to the queue connection when generating a .env file from the config files.
- The individual composer.json files for each of the October Rain library components have been removed as using individual components of the October Rain library is no longer supported.
- Support has been added for `hasOneThrough` relationships.
- Support has been added for the `eloquent.retrieved` Model event that Laravel added in 5.5.2.
- The `app:name` Artisan command was removed as Laravel removed it in L6 and October never really had a need for it.
- Added new public static method `Model::flushDuplicateCache()` to flush a given model's duplicate query cache during a request lifecycle.
- Added polyfill for the `http_build_url()` core PHP function.
- Added new `php artisan create:theme $code` scaffolding command.
- Added new `Arr::undot()` and `array_undot` helper methods / functions (transforms a flat, dot-notated array into a normal nested array)
- Added new `config_path()` helper function.
- Added new `resolve_path()` helper function that closely emulates the PHP `realpath()` function, but supports resolving paths for missing files and subdirectories. This is provided by the `October\Rain\Filesystem\PathResolver` helper class, which can resolve canonical paths and determine if given paths are within given directories.
- The `October\Rain\Database\Attach\File` model now uses "fillable" attributes as opposed to "guarded" attributes to control mass assignment. If you extend the `File` (or the main `System\Models\File`) model to provide additional fields, you must now copy the "fillable" attributes to your extension and add any additional fields to this definition.
- The `October\Rain\Database\Attach\File` model will now log exceptions when `getThumb()` fails in addition to generating the broken image file as the thumbnail as per existing behaviour.
- The `October\Rain\Html\HtmlBuilder::limit()` method now considers whitespaces and line breaks to be one character, regardless of the line break type or number of spaces. This ensures a consistent result across both Windows and Linux.

## Bug Fixes
- Improved stability of the FieldParser when parsing fields without the type property specified.
- Fixed issue where the `QueryBuilder->remember()` method did not properly support being passed DateTime instances for cache expiry.
- Fixed an issue introduced in Build 466 where asset files were unable to be created through the CMS section.
- Fixed issue where removing the currently sorted by column from the list's visible columns would cause an error.
- Fixed issue where not having the GD extension loaded would cause the process to exit with an error message instead of throwing an Exception.

## Security Improvements
-

## Translation Improvements
- Improved Spanish translations.

## Performance Improvements
-

## Community Improvements
- Added the Laravel framework dependency to each of the core modules to improve stability of existing composer installations
- The `ftp` and `sftp` storage drivers are now included with the core.
- The `postmark` mail driver is now included with the core.
- The October CMS and Rain Library are now tested against both Linux and Windows, PHP versions 7.2 to 7.4, to ensure that functionality works correctly across both supported operating systems.

## Dependencies
- The Laravel framework has been added as a dependency to the core modules and library to improve the stability of existing Composer installations.
- The Assetic library is no longer an external dependency as the key functionality has been absorbed by the October Rain library.
- The unmaintained `leefo/scssphp` dependency has been replaced with `scssphp/scssphp`
- The unmaintained `lessc.inc.php` included dependency has been replaced with `wikimedia/less.php`
