# Build 1.2.7

## UX/UI Improvements
- Checkbox lists will now show all of their options, even when disabled or in read-only mode.
- Visiting the backend login page will now redirect to the backend dashboard if the user is already logged in.
- Added additional warning about disabling debug mode in production to the `config/app.php` file.
- Added additional configuration checks to the Status dashboard widget.
- Improved the UX of drag and drop sorting of tree views.
- Disabled autocomplete on `password` and `sensitive` field types by default.
- Added new `user:create` CLI command to create a new backend user from the CLI.
- Added support for the AJAX Framework Extras (`attach-loading`, etc) to be used in the backend.
- Fixed minor box shadow issue with the recordfinder clear button.
- Made the entire fileupload field clickable in single file mode.
- Repeater items can now be extended by clicking on their title rather than just the dropdown arrow.
- Fixed minor styling issues with Select2 inputs.

## DX Improvements
- Added support for the [Vite](https://vitejs.dev/) asset compiler (see [Laravel docs](https://laravel.com/docs/11.x/vite) & [Winter docs](https://wintercms.com/docs/develop/docs/console/asset-compilation-vite) for more information).
- Added new `npm:install`, `npm:update`, `npm:run` helper CLI commands. Refer to [the docs](https://wintercms.com/docs/develop/docs/console/asset-node-utilities).
- Added new `BundleManager` that manages the "asset bundles" used by the `mix:create` and `vite:create` scaffolding commands.
- Added support for Laravel-style relations (see https://github.com/wintercms/docs/pull/176)
- Added a simple `.devcontainer` for the Storm library and the main Winter repository.
- Added support for "asset prioritization / load ordering" to the `AssetMaker` trait through the use of a new `order` system attribute that can be provided.
- Added support for project relative paths to the SQLite database.
- Changed the default scaffold for `create:theme` to Tailwind
- Added support for all `abort($code)` errors to the CMS module, now you can use `abort(404)` anywhere and get a nice 404 error page.
- Added `winter:install`, `winter:env`, and `winter:mirror public` to the default post create project composer scripts.
- Improved compatibility with Laravel's `artisan migrate` command by adding support for the `--seed` option.
- Added support for using dynamic methods to handle custom list column types.
- Added `create:factory` command to scaffold model factories in plugins.
- Added support for the `--batchable` option to the `create:job` scaffolder.
- Added support for dynamically extending filter scopes even if no scopes have been defined yet.
- Added `--sidebar` flag to the `create:controller` scaffolder to create a controller that uses the sidebar layout for form views.
- Fixed display of deleted files when reviewing changes in `winter:version`.
- Added `--only-version|-o` option flag to `winter:version` to display only the version number.
- Added new `winter:util purge resized` CLI command to delete all previously cached images from the resizer.

## API Changes
- Added support for `.avif` image files.
- Removed the unnecessary Maker class from the core Application container.
- Added support for `$table->dropColumnIfExists()` in migrations.
- Added support for enabling the Laravel Mix manifest feature.
- Added `File::getMaxUploadSize()` and `File::sizeToBytes()` helper methods.
- Added `slave` relationship configuration to the `DeferredBinding` base model.
- Added `$routePersistance` parameter to `Page::resolveMenuItem()`.
- Removed unnecessary `TableData` prefix from data returned by the Table widget (also `DataTable` formwidget) in AJAX requests.
- Added support for translation strings providing options in `FormField->options()`.
- The Stripe Loader provided by Snowboard.js can now be disabled by setting `data-request-stripe` to false.
- Added support for command names that include a number.

## Bug Fixes
- Fixed the argument order for `paginate()` and `simplePaginate()` in `BelongsToOrMorphsMany` relationships.
- Fixed issue where attempting to use the `SortableScope` could conflict with columns in pivot tables.
- Fixed infinite loop when using `HasSortableRelations` on a model with a self-referencing relationship.
- Restored the previous default value of true for `showPageNumbers` in the `RelationController`'s `view` and `manage` configuration scopes.
- Fixed support for empty calls to `date()` in Twig.
- Fixed issue where FormWidgets would return null even when their raw field values aren't present in the save data.
- Fixed issue with some styling elements in the backend due to the switch of asset compilation systems for the backend styles in 1.2.6.
- Fixed error when using taglist with a single value.
- Fixed issue where the `RelationManager` FormWidget was overriding the default configuration of the `RelationController` even when the overrides were not explicitly set on the field instance.
- Fixed issue where creating themes from the backend using the `blank` scaffold would fail.
- Fixed issue where custom File models could not use string keys (i.e. UUIDs) as their primary key when using the default backend partials.
- Fixed issue where Pivot models were not being properly initialized with their attributes causing problems when the pivot record contained `jsonable` attributes used by repeaters / nested forms.
- Improved `trace_log` helper's handling of objects
- Fixed support for viewing complex (jsonable) pivot data in the RelationController.
- Fixed issue where the job class was generated twice when using `create:job` with the `--sync` option.
- Fixed issue where `maxItems: 1` didn't work for the first item on repeaters.
- Fixed nested form data in Snowboard requests.
- Fixed issue where the Mix webpack config wasn't being removed after it was no longer required.

## Security Improvements
- Added the `$requiredPermissions` property to the default controller stub used by `create:controller`.
- Hardened theme objects, preventing certain properties from being passed through to the ThemeData object.
- Improved the Twig security policy (blocked methods that write, delete, or modify records and attributes in Database/Eloquent and Halcyon models; blocked access to the theme datasource; prevented extensions from being created or directly interacted with).

## Translation Improvements
- Improved Latvian translation.
- Improved French translation.
- Improved Russian translation.

## Performance Improvements
- `Winter\Storm\Database\Traits\ArraySource` now supports using generators to return records in the `getRecords()` method.

## Community Improvements
- Fixed links to documentation in `composer.json`

## Dependencies
- Bumped minimum required version of Twig to v3.14 to fix potential security issue.
