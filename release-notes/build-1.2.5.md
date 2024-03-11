# Build 1.2.5

## UX/UI Improvements
- Added support for mass enabling / disabling of permissions in the PermissionEditor FormWidget by clicking on the column headers.
- Added support for `allowCustom` in dropdown fields to allow for custom values to be entered by the user.
- Added support for `balloon-selector` fields as `titleFrom` sources in Repeaters.
- Added support for custom disks in the `winter:util purge uploads` command.
- Removed the unnecessary `<p>` tag from the email button partial.
- Added disabled state styling for switch fields.
- Added dynamic file extension icons to the Media Manager for files without thumbnails.

## API Changes
- Increased the default cache time of CombinedAssets to the 1 year, the current Google recommendation, instead of the previous recommendation of 1 week.
- The `.env.example` file will no longer be automatically copied to `.env` on project creation.

## Bug Fixes
- `Winter\Storm\Database\Attach\File` will now correctly respect the visibility property set on the disk configuration when storing files on the disk.
- Improved support for legacy plugins directly using the `October\Rain\Extension\ExtendableTrait` trait.
- Improved the HTML Helper's `reduceNameHeirachy()` method's ability to handle field names from nestedforms.
- Fixed support for `dynamicProperties` on PHP 8.2+ by no longer actually setting the properties on the object but instead using the existing `dynamicProperties` store to manage the values.
- `Event::forget()` now also removes prioritized event listeners.
- Fixed parameter typing for the `Http::data()` method that was causing issues on the Plugin Updates page.
- Improved support for reordering records in the backend when the sort order values on the existing records are in an inconsistent state.
- Improved support for PHP 8.2+ by replacing deprecated usage of `${}` in strings with `{$}`.
- Improved support for PHP 8.3 in the migration system.
- Improved support for `BackedEnum` values in the `FormField`'s `isSelected()` method.
- Improved support for arbitrary depth of `dependsOn` in backend fields.
- Fixed issue where null values passed to the `md` Twig filters would cause an error.

## Translation Improvements
- Added localization support for the System DateTime helper's `timeTense()` helper.
- Added lang keys to plugin controller scaffolding.

## Community Improvements
- Winter CMS is a Community Sponsor of Laracon US 2024.

## Dependencies
- Updated jQuery to 3.7.1 and jQuery Migrate to 3.4.1.
