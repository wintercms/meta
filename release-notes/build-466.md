# Build 466 (WIP)

## UX/UI Improvements
- Improved the disabled styling of the `markdown`, `richeditor`, `mediafinder`, & `colorpicker` FormWidgets.
- Fixed long standing issue where on initial page load the backend nav bar would be an incorrect width until the JS loaded to correct it by switching to a flex layout for the backend nav bar.
- Improved UX when an AJAX request is made while the application is in hard maintenance mode (`php artisan down`).
- Added three preset buttons (Default, Full, & Minimal) to the backend richeditor toolbar settings to simplify the experience of selecting a custom richeditor toolbar.
- Form tabs in the backend are now tracked in the URL bar by default making linking to specific tabs easier and retaining the place of the currently active tab across page reloads. Disable this behaviour by setting `linkable: false` on the form tab configuration.
- Added button on backend user record pages that allows admins to unsuspend a user account that has been locked out due to failed login throttling.
- AJAX requests will now attempt to perform HTML5 validation if present & supported by the browser before submitting the AJAX request.

## API Changes
- Menu items controlled by `NavigationManager` are now objects, and `$manager->getMainMenuItem($owner, $code)` has been added to make it easier to manipulate existing menu items without having to deregister and reregister menu items to apply changes.
- The `postbackHandler` property for DataTable form widgets now defaults to `null` - the widget will interpret a `null` value as to detect the save handler for the form that contains the widget (this is usually `onSave`, the old default value, but it will now detect other handlers such as those used by the relation controller).
- The `getParameter` method in `Cms\Classes\Router` is now correctly type-hinted.
- External parameters may now use dot notation to get a deeper-nested value when used for component parameters in a CMS object.
- Added `auth.throttle.*` configuration options to configure the login throttling for the backend.
- Added `formGetRedirectUrl($context, $model)` method to the `FormController` behavior, overrideable by the implementing controller. Used to get the redirect URL for a given context & model if a redirect is requested.
- If uploaded files are missing an extension October will now try to automatically determine one based on the MIME type of the file.
- Added support for the `attributes` property on the `colorpicker`, `codeeditor`, `markdown`, `richeditor`, `mediafinder`, & `fileupload` FormWidgets.
- Added support for the `placeholder` attribute on the `password` field type.
- Added support for defining custom values for the `title` and `toolbarButtons` labels of the RelationController behavior.
- Added support for a `badge` property on main & side menu items in the backend to display string values as the menu item badge instead of the only numeric values already supported by the `counter` property.
- Added a unique HTML id attribute to the Filter widget popups for targeting individual filter scopes in CSS.
- Added `usingSource($source, $closure)` method to the `Cms\Classes\AutoDatasource` to force the `AutoDatasource` to only use the specified source for that closure.
- Media items now only return an absolute URL if either `cms.linkPolicy` is set to `force` or the `path` property of the media storage disk starts with an absolute URL. This limits the breaking change from Build 444 to only installations using a `force` link policy.
- Implemented the new `Backend\Traits\UploadableWidget` trait intended for Widgets that need to handle uploading files to the Media Library.
- Added support for "soft" or "optional" components, a way for themes to include components only if they're present without breaking the theme if the relevant plugin is not installed and / or enabled. To make a component "soft" or "optional", prefix its name with `@`. Example: `[@staticPage]`
- Added support for `ignoreTimezone` to `date` and `daterange` filter scope types.

## Bug Fixes
- Fixed an issue where data in a DataTable widget inside a relation model popup form would not be saved on submit.
- Record Finder widgets will now correctly save and load a record when using a column other than ID in the `keyFrom` configuration value, when the widget is not in relation mode.
- Fixed issue where custom validation rule strings starting with `unique` would not register correctly.
- Fixed `propertyExists()` method to correctly detect properties added through `addDynamicProperty()`.
- Fixed `options` support for `checkboxlist` and `balloon-selector` field types in the Syntax Parser
- Fixed issues with properly quoting values when running `october:env`
- Fixed issue where Excel wouldn't properly detect the encoding of CSV files exported using the `useList` option
- Changed optional .htaccess line forcing HTTPS to default to returning a 301 response instead of 302.
- Asset files uploaded in the CMS will now take their default permissions from the value set in the configuration.
- Repeaters will now trigger `change.oc.formwidget` when adding or removing items.
- Fixed issue where the richeditor toolbar popups were z-index clashing with other form elements.
- Fixed issue where mail layouts that didn't exist in the database but did exist in the filesystem weren't being loaded correctly.
- Fixed issue where some browsers would incorrectly check off list checkboxes after a page reload through the autocomplete functionality which would cause visual & behavioural inconsistencies.
- Fixed support for importing CSV files with encodings not supported by `mb_convert_encoding()` by using `iconv()` as a fallback.
- Fixed issue where translations for related models managed by the `RelationController` behavior would not save when creating the related model, or updating a pivot model.
- Fixed issue where model scopes applied by the `relation` FormWidget didn't support joins being used.
- Fixed issue where `php artisan theme:sync --target=database` wouldn't properly sync to the specified target.
- Improved the flexibility of the PluginManager in accepting plugin identifiers that are not perfectly matched to the desired plugin's casing (i.e. `Rainlab.Blog` would be considered an invalid plugin identifier prior to this change, it is now correctly identified as belonging to `RainLab.Blog`).
- Fixed issue where pivot records being created or updated through the `RelationController` would not trigger the form field change events.
- Update manager now respects the values of `cms.pluginsPathLocal` and `cms.themesPathLocal` when installing new plugins & themes.
- Improved support for opcache when `opcache.restrict_api` is in effect.
- Fixed issue where `Lang::choice` method would not use the plural form for a locale with a sublocale (ie. "English (United Kingdom)" / `en-uk`).
- Fixed issue where `theme:install` Artisan command would throw an exception if the database templates feature was enabled.
- Fixed issue where using the search query input in a filter for a relation list modal would throw a "not bound to controller" exception, due to the request not being tied to the relation list modal.
- Fixed weird outline styling around `:focus`ed elements introduced in Build 465

## Security Improvements
- Fixed vulnerabilities that required the `cms.manage_assets` permission to execute (local file inclusion, arbitrary file deletion, & arbitrary upload of asset file types). Credit to [Sivanesh Ashok](https://twitter.com/sivaneshashok) for the discovery.
- Fixed vulnerability where maliciously crafted CSV files could lead to a self-XSS attack when using the `ImportExportController` behavior. Credit to [Sivanesh Ashok](https://twitter.com/sivaneshashok) for the discovery.
- Prevented potential CSV injection attacks via the `ImportExportController` behavior. Credit to [Sivanesh Ashok](https://twitter.com/sivaneshashok) for the discovery.

## Translation Improvements
- Improved German translation.
- Improved Russian translation.
- Improved Hungarian translation.
- Improved Slovenian translation.

## Performance Improvements
- Minor performance improvement by not calling Lang::get() every time a CMS Page object is instantiated.
- Minor performance improvement in the plugin manager by not looping over all plugins everytime a plugin identifier needs to be normalized.

## Community Improvements
-

## Dependencies
- Switched from the abandoned `jakub-onderka/php-parallel-lint` library to `php-parallel-lint/php-parallel-lint` for code linting purposes in the October CMS and Rain library test suites.
- Locked the wikipedia/composer-merge-plugin dependency to version 1.4.1.
