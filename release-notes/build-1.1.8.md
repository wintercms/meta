# Build 1.1.8 (WIP)

## UX/UI Improvements
- All default backend controller behaviors (i.e. `FormController`, `ListController`, `RelationController`, etc) no longer require a configuration property (i.e. `$formConfig`, `$listConfig`, `$relationConfig`, etc) defined on the implementing controller if the default config file is being used (i.e. `config_form.yaml`, `config_list.yaml`, `config_relation.yaml`, etc).
- The `winter:down` command now requires a user to explicitly confirm the action by typing `DELETE` in their CLI.
- The `plugin:remove` command now requires a user to explicitly confirm the action by typing the plugin code in their CLI.
- Added Created At & Updated At columns to the Backend User & User Roles lists, marked invisible by default.
- Updated the syntax highlighting language used by the backend custom CSS brand setting to acurately reflect the actual language in use (LESS, not CSS).
- The Markdown editor will now add a `https://` template when adding a link or image, to encourage use of secure links.
- Removed the timeout when running `winter:test`.
- Fixed styling issue with color pickers on the Mail Brand Settings page in the backend.
- Files in the CMS Theme Editor AssetList component will now be sorted alphabetically.
- Added ability to manage the list of users associated with a given role from that role's update page.
- Added "slug" input preset to the Administrator Role's code field.

## API Changes
- Permissions registered without the `roles` property defined will now only be inherited by the `developer` system role, not all system roles.
- Added [Snowboard.js](#todo), a new JS framework intended to replace the existing [AJAX Framework](#todo) that is more modular and no longer depends on jQuery.
- Added support for Laravel Mix via the following commands: [`mix:install`](#todo), [`mix:compile`](#todo), [`mix:watch`](#todo), & [`mix:list`](#todo).
- Added `System\Classes\MixAssets` singleton for managing an instance's Laravel Mix assets, see [`registerMixAssets()`](#todo) now available as a registration method for `Plugin.php`, `MixAssets::registerCallback()` for Modules, and the [`mix` property on `theme.yaml` definitions](#todo)
- Classes implementing the `System\Traits\PropertyContainer` trait to provide dynamic property options for Inspector fields no longer need to have zero (or one optional) parameters in their constructor in order to work correctly. Note that if your constructor requires a value in any property and does not define a default, this will still fail, so ideally you should still use a class specifically set up for handling Inspector properties.
- Added `| md_line` Twig filter to make use of the `Markdown::parseLine()` method in Twig templates.
- Replaced `Winter\Storm\Auth\AuthException` with `Winter\Storm\Auth\AuthenticationException`, added `Winter\Storm\Auth\AuthorizationException`.
- The `plugin:remove` command now provides a `--no-rollback` option which disables the rolling back of database migrations for a plugin when it is being removed, allowing the plugin data to be retained.
- Added support for the `app.asset_url` & `ASSET_URL` configuration options for use with the `Url::asset()` & `asset()` helpers.

## Bug Fixes
- Integers can now be used as values for options provided to the Inspector `set` field.
- Fixed issue with list of available encodings for importing where ISO 8859-9 was incorrectly referenced as ISO 8859-0.
- Fixed issue that could occur when running console commands on a project that had replaced plugins and their replacing plugins present at the same time.
- Fixed incorrect exception message when attempting to impersonate a user without authorization.
- Fixed color picker widget not allowing empty values.
- Fixed color picker widget showing misleading mouse cursors in read-only mode.
- Fixed color picker widget not triggering dependent fields on change.
- Fixed issue where attempting to render a theme without a database present would fail because the AssetMaker trait was attempting to get the system build information from the database even though the DB wasn't present.
- Fixed PHP 8 compatibility issue where a component with no controller throws an error when checking the existence of a method on the non-existent controller.
- Fixed bug introduced in v1.1.5 where an infinite loop would occur when attempting to impersonate a backend user while logged in as a user without the `is_superuser` flag.
- Modules will now be seeded before plugin migrations are run to support plugin migrations that interact with module seeded data.
- Fixed issue where setting the `readOnly` property to `true` on `datepicker` FormWidgets would leave the field greyed out but still editable.

## Security Improvements
- Improved the Twig SecurityPolicy to block more potentially dangerous entry points from being abused by accounts with access to Twig but not PHP.
- Themes can no longer be imported while `cms.enableSafeMode` is active.
- Added a warning message to the system status dashboard widget when the default admin user is detected on the system.
- Limited inheritance of "orphaned" (permissions without default roles assigned) to just the "Developer" role instead of all system roles.
- Fixed issue where users without the `backend.access_dashboard` could still access the dashboard if they did not have access to any other main menu items in the backend.

## Translation Improvements
- Improved Latvian translation.
- Improved Ukrainian translation.
- Improved French translation.
- Improved Italian translation.
- Improved Slovak translation.
- Improved Russian translation.
- Improved Persian translation.
- Improved Japanese translation.

## Performance Improvements
-

## Community Improvements
- [`Winter.Notes`](#todo), a new first party plugin for adding notes to any record type in Winter was released. It provides a custom `notes` FormWidget that presents a note management experience similar to the Mac OS Notes App.
- All code examples in the official documentation now has proper language highlighting depending on the language of each example.
- The console commands documentation has been signficantly refactored with an introductory page with a list of all commands now available. Commands are now grouped by their logical function.
- Added a default [`.vscode/settings.json`](#todo) to the project to help VS Code correctly identify the language (PHP, Twig, or WinterCMS Template) used for `.htm` files based on where in the project they are located.
- Added a default [`.vscode/extensions.json`](#todo) to the project to provide recommendations on extensions for VS Code that work well with Winter

## Dependencies
- Laravel 6.x LTS does not support PHP 8.1 so Winter has limited the supported PHP versions to PHP 7.2.9 -> PHP 8.0.*. PHP 8.1 support will come with Winter 1.2 using Laravel 9.x LTS in January 2022.
