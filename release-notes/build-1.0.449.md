# Build 1.0.449:

## UX/UI Improvements:
- Redirect users with the `manage_theme_options` (but not the `manage_themes`) permission directly to the Customize theme page
- Dashboard now uses a 12-column layout instead of a 10-column layout
- Show a "not found" message when the image selected by a `mediafinder` FormWidget does not exist
- Added link to backend updates page to see a detailed changelog for the current build
- Minor improvements to the styling of the clear search button

## API Changes:
- Support `enableDefaults` on repeaters using grouped mode
- Simplified the `Repeater` item's data saving process by calling each item's `Form` widget's `getSaveData()` method instead of attempting to process the data directly.
- Disabled `FormWidget`s are now ignored in the `Form` widget's `getSaveData()` method just like regular form fields are.
- Backend Controller middleware support has been changed to only support 'after' middleware as it requires instantiating plugin controllers in order to retrieve the middleware that they have registered, which calls the constructor for those controllers; which is where the problem is (Controller constructors often, for one reason or another, do things that require the session to be started, for instance, getting the current user)
- Added support for `headCssClass` in the `Lists` widget's column definitions to specify a CSS class to be added to the table header cell for that column.
- Added `allowTrashedSlugs` property to models that use the `Sluggable` and `SoftDelete` database traits to include the slugs of records that have been soft deleted when checking to see if a slug already exists.

## Bug Fixes:
- Fixed Save & Close button on the `ThemeOptions` update view
- Fixed long standing issue with being unable to update translated values with the RelationController
- Fixed issue where Repeaters with the same field names being bound to the same controller would cause confusing conflicts as they tried to process each other's data.
- Fixed issue where having the CMS module present but disabled would still try to handle backend 404's with the CMS controller.
- Fixed issue where multiple `Filter` widgets could not exist on the same page at the same time.
- Fixed support for migration files with extra `.`s in their file names (ex. `1.0.5.update_posts.php`)
- Fixed issue where the popup loading indicator would sometimes not close after the request had finished loading
- Improved FireFox & IE11 support by fixing race conditions in backend JS

## Translation Improvements:
- Improved French translation

## Community Improvements:
- Added guidelines for updating JS dependencies used in the Winter CMS core

## Dependencies
- Fixed issue with Twig 2.7.4
- Replaced all deprecated Twig PSR-0 class references with the new PSR-4 class references.
- Updated Froala to 2.9.3