# Build 1.2.4

## UX/UI Improvements
- `theme:list`, `plugin:list`, and `mix:list` now display nicely formatted tables.
- Added support for "grid" repeaters via new `mode: grid`, `columns`, and `rowHeight` options.
- Added new Asset URL helper to Snowboard.js: `Snowboard.url().asset()` that will use the configured `app.asset_url` value to generate URLs to asset files.
- Field option values can now be specified as a language key that points to an array of keys & values that will be automatically translated (ex. `options: author.plugin::lang.departments`).
- The MediaManager's sort type, direction, and view mode are now persisted to the user's preferences keyed by the usage of the media manager (i.e. all mediafinder usages are one key, the main media library is another). This means that the media manager will now remember your preferences between logins and in different contexts. The preferences are still overridden on a per-session, per-instance basis.
- Improved the error message when attempting to register an invalid extension to Twig (i.e. a non-callable extension).
- Added support for overscrolling in the `codeeditor` FormWidget via the `scrollPastEnd` option that allows the editor to scroll past the end of the document by the specified number of lines.
- Added a "Refresh" button to the RelationController.
- Toolbar widget will now only render its container HTML when it has at least one sub-widget to display.
- Minor styling improvements to the FileUpload thumbnail styles.
- Added new `RelationManager` FormWidget to simplify rendering the `RelationController`.
- Improved progress bar styling within List widgets.
- Added support for populating migrations created via `create:migration` with columns defined from the field configuration for the provided model.
- Added support for `showSetup` in list views of the RelationController.

## API Changes
- Added the `bootstrap/cache` folder to the `wintercms/winter` repo as it is expected to exist by Laravel core commands related to caching.
- When running any commands from the CLI while your application has a database connection configured but the `migrations` table is not yet present on it, the application will also be considered in a protected state and only [elevated plugins](https://wintercms.com/docs/v1.2/docs/plugin/registration#elevated-permissions) will be loaded. This is to prevent issues with commands that may attempt to access the database before migrations have been run.
- `filterFields()` and `model.filterFields()` will now be called immediately before the `Form` widget returns the save data in `getSaveData()`.
- New partials have been added to the `RelationController` to enable more easily extending the default footer used in `RelationController` modals.
- The application container will now create cache directories if they don't exist for anything passed to `App::normalizeCachePath()`.
- Added support for the `event:cache`, `event:clear`, and `event:list` commands.
- Added `App::hasDatabaseTable()` helper to check if the configured database connection has a specific table.
- Added `Model::hasDatabaseTable()` and `Model->isDatabaseReady()` helpers to check if the model's table is present in the model's database connection.
- Added `Model->hasAttribute($attribute)` helper to check if the provided attribute would be processed by the model's `getAttributeValue()` method (i.e. it exists in `attributes`, is castable, or has a mutator / accessor).
- Added the `json()` helper to the `Http` network utility class to send requests with a JSON body.
- Added support for the `limit` property on list column relation value queries.
- `develop.debugSnowboard` will no longer fallback to the value of `app.debug`, instead it will default to `false`.
- `CmsObject::listInTheme()` will no longer include null entries in the returned list.
- Variables shared via `View::share()` will now also be shared with CMS Twig templates as global variables.
- Added support for appending and prepending datasources to the AutoDatasource.
- Added support for soft deleting Backend User Groups.
- Added new `backend.list.extendColumnsBefore` event to match `backend.forms.extendFieldsBefore`.
- Added new `model.getValidationAttributes` event.
- Model event methods (i.e. `afterSave()`, etc) will now be bound to and fired by the event dispatcher instead of firing directly. This allows for more flexibility in the order of event listeners and allows for the event to be cancelled before reaching the original model listener method.
- Added new `Encryptable` database behavior that functions the same as the existing trait but can be dynamically applied to models.
- Improved automatic detaching / deletion of relations. Adds support for `deletedAtColumn` to relation pivot configurations.

## Bug Fixes
- Fixed an issue when attempting to access a `SettingsModel` after the database exists but before any migrations have been run.
- Fixed issue where Snowboard.js `extras` weren't being loaded from the configured `app.asset_url` when using custom CDNs.
- Mail template style tags are now put in the `<head>` element instead of the `<body>` element.
- Snowboard.js will now resolve promises even if the `beforeUpdate()` event is cancelled, which provides a way to cancel the updating of partials while still allowing the rest of the request lifecycle to proceed.
- Added support for setting `stripe: false` in the options for a Snowboard.js request when the snowboard extras are present to disable the stripe loading indicator for that request.
- Fixed an issue where Winter would fail to load on some systems when an `open_basedir` restriction was in place.
- Fixed an issue where the Repeater's `form` configuration wasn't allowing `stdClass` or `string` values.
- Fixed an issue where recompiling the backend styles would cause the User Impersonation Notice styles to be lost.
- Improved support for `BackedEnum` values in lists and forms.
- Fixed issue where asset URLs weren't being cached by the current host / scheme causing mixed type errors.
- Fixed issue where RichEditor popups (i.e. when inserting links) would open and then rapidly close when interacted with; caused by change events being fired on the editor when the popup was opened.
- Fixed issue where pages with no components would cause a crash when `getComponentProperties()` was called.
- Fixed issue where the `showTree` config value would be cleared when the search term was cleared instead of being preserved.
- Fixed issue where installing Winter in certain directories would fail to work.
- The in-memory DB cache will now be cleared when an upsert is performed.

## Performance Improvements
- Added indexes to the `sessions` table.

## Community Improvements
- Launched the rebuilt version of the [WinterCMS.com](https://wintercms.com) website and project documentation.
- Automated the generation of the build manifest file for new releases of Winter CMS.
- Added support for Block template files (`.block`, see [Winter.Blocks](https://github.com/wintercms/wn-blocks-plugin)) to the Winter CMS VS Code extension.
- Added link to get paid support from the core team to the Winter CMS website and repository.
- Improved support for dark mode on the [Winter.TailwindUI](https://github.com/wintercms/wn-tailwindui-plugin) plugin.
- Core team founded Frostbyte Foundation, Inc.; a non-profit incorporated in Canada to support the Winter CMS project and community.
