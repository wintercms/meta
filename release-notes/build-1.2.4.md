# Build 1.2.4 (WIP)

## UX/UI Improvements
- `theme:list`, `plugin:list`, and `mix:list` now display nicely formatted tables.
- Added support for "grid" repeaters via new `mode: grid`, `columns`, and `rowHeight` options.
- Added new Asset URL helper to Snowboard.js: `Snowboard.url().asset()` that will use the configured `app.asset_url` value to generate URLs to asset files.
- Field option values can now be specified as a language key that points to an array of keys & values that will be automatically translated (ex. `options: author.plugin::lang.departments`).
- The MediaManager's sort type, direction, and view mode are now persisted to the user's preferences keyed by the usage of the media manager (i.e. all mediafinder usages are one key, the main media library is another). This means that the media manager will now remember your preferences between logins and in different contexts. The preferences are still overridden on a per-session, per-instance basis.
- Improved the error message when attempting to register an invalid extension to Twig (i.e. a non-callable extension).

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


## Bug Fixes
- Fixed an issue when attempting to access a `SettingsModel` after the database exists but before any migrations have been run.
- Fixed issue where Snowboard.js `extras` weren't being loaded from the configured `app.asset_url` when using custom CDNs.
- Mail template style tags are now put in the `<head>` element instead of the `<body>` element.
- Snowboard.js will now resolve promises even if the `beforeUpdate()` event is cancelled, which provides a way to cancel the updating of partials while still allowing the rest of the request lifecycle to proceed.
- Added support for setting `stripe: false` in the options for a Snowboard.js request when the snowboard extras are present to disable the stripe loading indicator for that request.
- Fixed an issue where Winter would fail to load on some systems when an `open_basedir` restriction was in place.

## Security Improvements
-

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
- Launched the rebuilt version of the [WinterCMS.com](https://wintercms.com) website and project documentation.
- Automated the generation of the build manifest file for new releases of Winter CMS.
- Added support for Block template files (`.block`, see [Winter.Blocks](https://github.com/wintercms/wn-blocks-plugin)) to the Winter CMS VS Code extension.
- Added link to get paid support from the core team to the Winter CMS website and repository.
- Improved support for dark mode on the [Winter.TailwindUI](https://github.com/wintercms/wn-tailwindui-plugin) plugin.

## Dependencies
-