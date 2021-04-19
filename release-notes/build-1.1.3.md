# Build 1.1.3 (WIP)

## UX/UI Improvements
- Added support for choosing the default backend locale and timezone in `php artisan winter:install`.
- Controller scaffolding now uses the default backend localization keys for the default titles in the FormBehavior config instead of hardcoded English strings
- The `unique` validation rule can now be used without any additional information, previously it required the table name to be specified in the form of `unique:table_name`. This also means that `unique` validation rules will respect the current model's `$table` property.

## API Changes
- Added support for modifying the RichEditor's allowed attributes list through the EditorSettings in the backend
- Added support for lazy loading class aliases only when needed through the new `Winter\Storm\Support\ClassLoader->addAliases(['Real\Class' => 'Alias\For\Class'])` method.
- Added support for saving deferred bindings with pivot data.
- Added `Backend::makeCarbon($dateTime)` helper for setting the backend timezone on date values.
- Added support for Dependency Injection in console commands.
- Added support for `php artisan winter:util purge orphans` command that removes any `system_files` records that do not have matching files stored on the filesystem.
- Added support for `registerValidationRules` in the `Plugin.php` plugin registration file to register custom validation rules.
- Added support for specifying `min`, `max`, and `step` values on the `number` and `numberrange` List Filter scope types.
- Added support for translator namespace aliases by adding `Lang::registerNamespaceAlias('real.namespace', 'aliased.namespace')`.
- Added support for aliasing entire namespaces in the class loader via the new `Winter\Storm\Support\ClassLoader->addNamespaceAliases(['Real\Namespace' => 'Aliased\Namespace'])` method.
- Added support for pre and post processing of YAML being parsed which should pave the way for supporting YAML v4
- Added support for array views to the MailFake class
- Added support for HTTP HEAD requests from the `Http` utility.
- Added boolean `$ok` indicator to the `Http` utility to indicate if the last response was successful (ie. an HTTP 2xx response code was returned)
- Added support for automatic cache busting for the assets loaded by the `{% framework %}` Twig tag based on the current version stored in the database. Use `artisan winter:version` to set the correct version for your project.
- Added `Config::registerNamespaceAlias($original, $alias);` to allow aliasing a config namespaces to another config namespace, i.e. `Config::registerNamespaceAlias('winter.debugbar', 'debugbar');` would return the config items from `winter.debugbar` when accessing the `debugbar` config. This is useful for forked packages or when integrating Laravel packages into Winter.
- Added `Config::registerPackageFallback($original, $fallback)` to allow the config items to be loaded from the global `$fallback` config when present if the `$original` global config isn't present. Useful when forking plugins to ensure existing installations with customized configs at the global level continue to work.

## Bug Fixes
- Fixed issue with Schedule->withoutOverlapping() by bringing the Halcyon MemoryRepository more inline with the parent class.
- Fixed an error thrown when using the "package:discover" command when `app.loadDiscoveredPackages` set to false, as the manifest was reset to `null` as opposed to an empty array.
- Fixed issue where tooltips set on the first column of the Lists widget were not working.
- Fixed issue where components that used dependency injection in their constructors would break in the backend.
- The RecordFinder FormWidget will now automatically determine what to use for the key column if the model used is not using the default of `id`. This used to be controlled by the undocumented `keyFrom` option on the recordfinder, but is now handled behind the scenes automatically.
- Reverted "Fixed issue introduced in Laravel 5.7 where eager loading `File` relationships on PostgreSQL would fail with the message "Varchar <> Integer comparison is not allowed"" introduced in 1.1.2 since it was causing issues when strict typing was enabled.
- Fixed an issue where `PluginManager->getRegistrationMethodValues()` would attempt to call protected methods on PHP 7.4.
- Improved Media Library path validation logic by allowing `//` but not allowing `://` to account for poorly constructed paths that are still technically valid.
- Fixed issue where sending emails using the Laravel Notification system could cause an exception in the System module when it attempted to extend a view instance while it was expecting a view string reference.
- Fixed issue where a TagList field that is disabled or readOnly would fail to correctly render if the value was an array.
- Added branching support for `winter:version`, different version branches (1.0, 1.1, etc) can now be correctly identified.
- Improved handling of dates by the Filter widget, specifically when ignoreTimezone is set on only one of a few date inputs in a given filter, and when using the daterange filter type with certain date values.
- Changed the default value of `database.connections.sqlite.database` to `base_path('storage/database.sqlite')` to better support applications using a mirrored public directory.
- Fixed issue where redirects to slow loading pages via AJAX could stop the loading indicator (and thus enable the triggering element) before the redirect actually completed, potentially leading to users triggering multiple requests unintentionally. As a side-effect due to how browsers process file downloads triggered by AJAX, this broke the loading indicator for AJAX redirects that cause the browser to download files instead of leaving the page; see [the test plugin](https://github.com/wintercms/wn-test-plugin/commit/9fb25e233e5da16daead8c12526b69f4aca53a30#diff-acf973ac915a3ac625f316456994123c57a688463a4a74c31247cf6334643365R8-R15) for how you can manually fix that functionality within your projects.
- Fixed long standing issue with the pagelinks plugin in the richeditor where inserting a link from the pagelinks popup would insert it at the start of the content instead of where the selected text was, and fixed another issue that would cause any preset text to be overwritten when selecting a link to use from the pagelinks popup.
- Fixed issue where exceptions / errors that were thrown before the `Event` facade was available would always be reported as "Class Event does not exist" instead of the actual problem.
- Fixed support for CSS variables within the asset compiler / combiner, this is a step closer towards native Tailwind support within Winter CMS.
- Fixed issue where resizing certain `.gif` images would result in `imagecolorsforindex(): Argument #2 ($color) is out of range`.
- Fixed issue where resizing `.gif` images with no transparent colour set would result in the white colour being replaced with the default transparent colour.

## Security Improvements
- Improved password reset flow by no longer throwing an error message if the provided email address doesn't exist in the system.
- Tightened up the permission checking logic by requiring strict type matches.
- Removed `xml` from the list of default allowed extensions to upload, can be added back through the configuration if required.

## Translation Improvements
- Improved French translation.
- Improved Russian translation.
- Improved Dutch translation.
- Moved Media Manager `rename` and `move` action language keys to the backend module instead of the CMS module.

## Performance Improvements
-

## Community Improvements
- Documented the Lists widget's `perPageOptions` configuration property

## Dependencies
- Refactored the `Winter\Storm\Events\Dispatcher` class to extend and override the base Laravel Event Dispatcher rather than just duplicating and implementing the contract for greater compatibility with Laravel.
- Updated from `symfony/yaml` v3.4 to `symfony/yaml` v4.4 and added a default preprocessor to automatically fix breaking changes between v3 and v4 of the symfony/yaml package.
- Switched away from the abandoned `fzaninotto/faker` package to the maintained `fakerphp/faker` package.
