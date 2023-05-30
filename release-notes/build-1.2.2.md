# Build 1.2.2

## UX/UI Improvements
- Added support for Child Themes by defining a theme code in the `parent` property of a theme's configuration file (`theme.yaml`).
- Added support "virtual" themes (`theme.yaml` files present in the DatabaseDatasource when using the Database Templates feature).
- Added `iconpicker` FormWidget with support for custom icon libraries.
- Component assets stored in an `assets` directory within the component directory will now be mirrored by the `winter:mirror` command.
- The AJAX form validation feature [documented in Snowboard](https://wintercms.com/docs/snowboard/extras#ajax-validation) that was missed during the initial implementation of Snowboard is now included by default with the `extras` package.
- Lists can now be sorted by invisible columns.
- The `alert()` & `error()` methods on `Winter\Storm\Console\Command` now implement Laravel's CLI components for rendering messages.
- Number of items in a folder in the Media Manager is now correctly pluralized.
- Fixed the icon for the "Return to parent" folder item in the Media Manager.
- Tweaked sizing of the inputs for a `datepicker` field in `datetime` mode - the date input size has been slightly increased, and the time input size has been slightly decreased, to better fit their respective content.
- Checkbox fields marked required will now show the required indicator.
- Fixed issues with the fancy layout styles affecting nested form styles.
- Fixed issue where an empty option element was present when adding a widget to the dashboard.

## API Changes
- Vue 3 is now available in the backend via the `window.Vue` variable.
- Added new `slug` validation rule that validates a string as a valid URL slug (alpha-numeric and a defined separator, defaults to `-`).
- Added new `Str::isJson()` method to check if a string is valid JSON as well as the `is_json()` global helper function.
- Added new `File::isAbsolutePath()` method to the `Winter\Storm\Filesystem\Filesystem` class to check if a path is absolute.
- Added support for the `mode` property for the `mediafinder` FormWidget. Supported modes include: `image`. `video`, `audio`, `document`, `file`, and `all`.
- Added a new `metadata` JSON blob column to the `backend_users` table.
- Added support for extending the `head` block in the backend views via `Block::append('head', $html)`.
- Added `sizeBytes` and `lastModified` attributes to media items returned by the Media Manager's `getItems()` JS function.
- Added `$formWidget` as a variable made available to partial fields.
- Locally defined dynamic methods are now prioritized over behavior-defined methods, allowing you to override behavior methods in your Extendable classes.
- Added support for scoped dynamic code extension. You can now pass `true` as the second parameter to the `::extend()` static method in order to run extension code within the context of the class being extended giving the code access to protected and private properties and methods.
- Added support for local dynamic code extension. You can now call the `extend()` method on an instance of an Extendable class to have that extension apply only to that instance of the object.
- Refactored backend JS widget loading, added `backend.ui.eventHandler` and `backend.ui.widgetHandler` Snowboard plugins, refactored the IconPicker, ColorPicker, & Sensitive FormWidgets widgets as Snowboard plugins.
- Snowboard.js event listeners now support closures.
- A new configuration, `develop.debugSnowboard`, has been added to `config/develop.php`, to allow overriding if Snowboard debugging and console logging is enabled, independent of the `app.debug` setting.
- Added support for the `RESTRICT_BASE_DIR` environment variable to control the `cms.restrictBaseDir` config setting.
- The `content` function in Twig now can return a boolean, thus allowing usage as a conditional for fallback content if a content file does not exist.
- The `Markdown` parser now uses the [CommonMark library](https://commonmark.thephpleague.com/) by the PHP League, as this library is already a Laravel dependency.
- A `$settingsCacheTtl` property may be provided for models that implement the `SettingsModel` behavior. This property accepts an integer and allows you to set the length of time (in seconds) that settings in this model will be cached for, defaulting to 1440 seconds (24 minutes).
- Split the `render()` method of `Winter\Storm\Halcyon\Processors\SectionParser` into three methods (`renderSettings()`, `renderCode()`, and `renderMarkup()`) as well as added three methods for parsing the sections (`parseSettings()`, `parseCode()`, and `parseMarkup()`). This makes it much easier to extend the `SectionParser` to build customer parsers. Demonstrated in the [Winter.Blocks plugin](https://github.com/wintercms/wn-blocks-plugin).
- Added support for setting the cache key per instance of the AutoDatasource.
- Refactored the `ClassLoader` to support PSR-4 autoloading for packages added via the `autoloadPackage($namespace, $path)` method (modules & plugins). The old method of lowercase folders with proper case files is still supported as well.

## Bug Fixes
- Refactored the `Winter\Storm\Support\Traits\Singleton` trait to bind to the application container instead of the global scope, which was causing issues with running multiple instances of Winter CMS in the same PHP process (i.e. unit tests, Laravel Vapor, Octane, etc).
- Fixed an issue where `add()` and `remove()` methods on the `Winter\Storm\Database\Concerns\BelongsToOrMorphsToMany` relation were passing the model key instead of the model instance to the `attach()` and `detach()` methods.
- Fixed an issue with generating thumbnails on disks with custom `root` paths, also simplified the logic for generating thumbnails.
- Improved support for multiple database connections in a single Winter project by using the parent model's connection when creating a new model instance from a relation, specifically when using Deferred Binding.
- Fixed support for class castable attributes on models.
- Fixed support for `artisan route:cache`.
- Fixed issue where the `FormBuilder` would generate elements with empty `id` attributes.
- Improved support for asset URLs in multiple places.
- Fixed incorrect return type for the `onLoadMovePopup()` MediaManager AJAX handler.
- Fixed the usage of POST arrays when using the original AJAX framework, which sometimes were incorrectly collated by the nested parent forms functionality implemented in Winter v1.2.0.
- Fixed `depends` usage in the Inspector widgets for `object` and `objectlist` fields.
- Fixed issue where fields with the `slug` or `camel` preset tools enabled wouldn't respect the max length of the field.
- Fixed issue where backend permissions weren't being registered when in any context other than the backend.
- Fixed numerous instances of the `App` facade being used instead of the local reference to the `app` instance which should improve support for multiple instances of Winter CMS in the same PHP process.
- Fixed issue where contextual fields (`name@context`) could not be removed via `removeField('name')`.
- Fixed issue with the embedded JSON attribute parser treating datetime values as floats.
- Fixed incorrect usage of the `plugin:install` command inside the `winter:install` command, due to a change in the former command's parameters.
- Removed Winter.Drivers as a recommended plugin to install when running `winter:install`.
- Fixed incorrect URLs being returned by the `System\Models\File::getPublicPath()` method if the storage being used was not a local file storage.

## Security Improvements
-

## Translation Improvements
- Improved Russian translation.
- Improved Ukrainian translation.
- Improved Latvian translation.
- Improved French translation.
- Improved Italian translation.
- Improved Slovak translation.

## Performance Improvements
- Improved the performance of resolving the active theme in cases where there are a lot of themes present or "virtual" themes are being used.

## Community Improvements
- Added Emmet support to Winter CMS template files with the official Winter CMS plugin for VS Code.
- Improved examples in documentation for extending forms via the `form.extendFieldsBefore` and `form.extendFields` events.
- The `\TestCase` alias has been set up to point to the correct base test class for unit tests, removing the need for adding a polyfill class in unit tests to support testing in both Winter v1.1 and v1.2. By extending this alias, unit tests should now work in both branches.

## Dependencies
- Replaced the dependency on `erusev/parsedown` and `erusev/parsedown-extra` with `league/commonmark` for the Markdown parser which was already included by Laravel and improves compliance with the [CommonMark specification](https://spec.commonmark.org/).
- Testing suite is now running on PHP 8.0, 8.1, & 8.2 across Ubuntu & Windows.
- Updated `wikimedia/composer-merge-plugin` to `~2.1.0` to allow for the `replace` configuration of dependencies to be merged together.
