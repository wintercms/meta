# Build 1.2.8

## UX/UI Improvements
- Added a beautiful error log viewer in the backend that displays contextual information about exceptions, links directly to the source files, and unrolling of all previous exceptions in the stack.
- Added new `button` field type to make it easier to add custom buttons to backend forms.
- Added support for the `url` field type to the backend forms.
- Added email icon to `email` fields.
- Updated the default backend branding colours to match the Winter CMS Brand Guidelines.
- Added support for shift clicking to select multiple records at once in the Lists widget.
- Removed the sort icon from columns that aren't sortable and display a right arrow when a column is sortable but isn't currently being used to sort the results.
- Added `button-group` and `dropdown` filter scope types.
- Made the entire `mediafinder` field clickable when `mode: file`.
- Improve click behaviour of `recordfinder` fields when disabled.
- Allow users to zoom the backend on mobile.
- Added support for `abort(403)` to return the access denied view in the backend
- Improved handling of `abort(404)` in the backend
- Improved styling of disabled fields in the fancy form layout
- Hide the select all checkbox on the Lists widget when there are no records to select.
- Fixed anchor tag outline styling in Firefox.
- Style read-only columns on Table widget with slightly darker grey background to indicate read-only state.
- Allow tab and arrow navigation for read-only columns on the Table widget.
- Allowed searching option to show search box on the Table widget even if adding and deleting buttons are disabled.
- Fixed styling of toolbar on the Table widget if only the search box is shown (no background previously).
- Fixed styling of pagination on Table widget.
- Default to `ignoreTimezone = true` for date columns.

## DX Improvements
- Added default views for the following backend controller behaviors (FormController, ImportExportController, ListController, ReorderController)
- Backend controllers will now automatically set their navigation context in the form of `Author.Plugin` as the author, `$pluginName` as the main menu code, and `$controllerName` as the side menu code. This means that you can remove calls to `BackendMenu::setContext()` and constructor overrides in your controllers if they follow that convention.
- Improved styling of file generated / updated status message in scaffolding commands
- Added support for `ReactJS` in Vite & Mix compiled asset packages.
- Added support for customizing the Vite build directory.
- Improved support for [Model Factories](https://laravel.com/docs/9.x/eloquent-factories).
- Added `test` alias for the `winter:test` command.
- Added `schedule_timezone` property to `config/app.php`.
- Updated theme scaffold's README.md to reflect the use of Vite in the generated themes.
- Added `Mail::sendTo()` method to the Mail facade's docblock.
- Added support for modules to the `asset:create` commands (`mix:create`, `vite:create`).
- Make readOnly option case-insensitive on the Table widget.
- Improvements to the default scaffolding stub files to bring more inline with the future PSR-12 coding style update.

## API Changes
- **Added typehints to all the method signatures on the base `Winter\Storm\Database\Attach\File` model. (eg. `getPath()`, `getCacheKey()`, `getFilename()`, `getContents()`, `getDiskPath()`, `isPublic()`, etc).**
- Added `metadata` jsonable column to the base File model, migrations have been added for `system_files`, but if you use a custom files table you will need to add a migration that adds `$table->mediumText('metadata')->nullable();` to your files table.
- Made `getDiskName()` on the base `Winter\Storm\Database\Attach\File` model public.
- Added support for an array of names to use for the `postbackHandlerName` in the Table widget.
- Removed the `config:cache` command as it wasn't improving our performance and didn't fully work with Winter's flexible configuration system.
- Added support for `SystemException` and `ApplicationException` instances to define their own response codes.
- Added `appendViewPath()` and `prependViewPath()` to the `System\Traits\ViewMaker`. `addViewPath` is renamed to `prependViewPath()` and is for paths that have higher priority than the existing paths while `appendViewPath()` is for paths that should have lower priority than the existing paths (i.e. fallbacks).
- Behaviors extending `Backend\Classes\ControllerBehavior` will now automatically append their `views` folder to the controller's view paths allowing them to provide fallbacks for any views required by the behavior.
- The `create:controller` command will now no longer generate the views by default unless `--stubs` is also passed and the `--sidebar` flag is replaced with a `--layout=(standard|sidebar|fancy)` option to choose the form layout to use.
- Support for passing `new: true` as a parameter in the request body to `onSave()` calls that will return a redirect to the `create` action
- `formMakePartial(string $partial, array $params = [])` to the `FormController` behavior that will render a partial through the controller's `makePartial` using the following priority list of contextual names (`form_$context_$partial`, `form_$partial`, `$partial`).
- Added `PromptsForMissingInput` to the base `Winter\Storm\Console\Command` class.
- Removed the unused (and broken) `Winter\Storm\Database\DataFeed` class.
- `PluginTestCase` now resets the application router in the `setUp()` method between test runs to ensure that plugin routes load in the correct order during tests.

## Bug Fixes
- Removed redundant backend route.
- Fixed issues where TagList & Repeater FormWidgets were not able to save an empty value.
- Fixed issue where TagList could return an object in array mode.
- Fixed using Vite packages when they are explicitly ignored / excluded from the project's `package.json`.
- Improved support for `winter:mirror` on Windows
- Using the `{% flash %}` tag in Twig will now properly purge the FlashBag after it has been read.
- Improved support for plugins attempting to access the database before it's fully ready to go.
- Fixed suport for hex colors with alpha values.
- Fixed infinite loop that occurrs when the configured database exists but the tables don't exist yet.
- Fixed support for array callables as dynamic methods.
- Event listeners bound to events with `bindEventOnce()` now properly unbind after execution, even if the event is a halting event.
- Fixed Syntax Error in CAST Statement for Postgres attachment.
- Fixed CMS Maintenance Mode not working when the `allowed_ips` setting has a value but a null list of IPs.
- Fixed CMS Maintenance Mode settings page not showing the correct value for when the Maintenance Mode is enabled.
- Improved support for using hasManyThrough / hasOneThrough relationships with soft deletes.
- Fixed support for the `--force` flag in `winter:env`.
- Improved support for defining multiple Vite entrypoints.
- Prevent crashes when rendering invalid values in datepicker fields.
- Prevent editors from being created for all column types in the Table widget if read-only (previously, only string columns would be rendered read-only by setting the readonly attribute, this is not ideal because it can be easily changed).
- Fixed broken search if client datasource is used on the Table widget.
- Fixed addVite() method not being able to bind assets to the parent controller.
- Fixed displaying the status of maintenance mode triggered through the backend.
- Fixed backend-triggered maintenance mode support for defined but empty IP lists.
- Fixed support for hex colors with alpha values in the `colorpicker` FormWidget.
- Improved handling of registering / booting plugins when migrations haven't been run yet.

## Security Improvements
- Added AllowList functionality to the Twig security policy.

## Translation Improvements
- Improved Russian translations.
- Improved Dutch translations.

## Performance Improvements
- Switched to a number input instead of a select dropdown for direct navigation to list pages in the Lists widget. Drastically improves performance when a list has 100+ pages in the results as it no longer causes an N+1 performance issue of rendering a single option element for every single page in your results.
- Fixed an infinite loop that could occur when a database was present but plugin migrations hadn't been run yet.

## Community Improvements
- Added Laravel to the list of organizational sponsors.
- Removed Route4Me from the list of organizational sponsors.

## Dependencies
- Added support for PHP 8.4
- Dropped support for PHP 8.0, PHP 8.1 is now the minimum requirement.
- wikimedia/less has been bumped to v5 from v3.
- Minimum Laravel version has been bumped to `v9.49`.
