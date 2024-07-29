# Build 1.2.7

## UX/UI Improvements
- Added support for the [Vite](https://vitejs.dev/) asset compiler (see [Laravel docs](https://laravel.com/docs/11.x/vite) & [Winter docs](https://wintercms.com/docs/v1.2/docs/console/asset-compilation-vite) for more information).
- Checkbox lists will now show all of their options, even when disabled or in read-only mode.
- Visiting the backend login page will now redirect to the backend dashboard if the user is already logged in.
- Added additional warning about disabling debug mode in production to the `config/app.php` file.
- Added additional configuration checks to the Status dashboard widget.
- Improved the UX of drag and drop sorting of tree views.
- Disabled autocomplete on `password` and `sensitive` field types by default.
- Added new `user:create` CLI command to create a new backend user from the CLI.
- Added support for "asset prioritization / load ordering" to the `AssetMaker` trait through the use of a new `order` system attribute that can be provided.

## API Changes
- Added support for `.avif` image files.
- Removed the unnecessary Maker class from the core Application container.
- Added support for `$table->dropColumnIfExists()` in migrations.
- Added support for enabling the Laravel Mix manifest feature.

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

## Security Improvements
-

## Translation Improvements
- Improved Latvian translation.
- Improved French translation.
- Improved Russian translation.

## Performance Improvements
-

## Community Improvements
- Fixed links to documentation in `composer.json`

## Dependencies
-