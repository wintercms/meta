# Build 1.2.8

## UX/UI Improvements
- Made the entire `mediafinder` field clickable when `mode: file`.
- Improve click behaviour of `recordfinder` fields when disabled.
- Allow users to zoom the backend on mobile.
- Updated the default backend branding colours to match the Winter CMS Brand Guidelines.
- Added a beautiful error log viewer in the backend that displays contextual information about exceptions, links directly to the source files, and unrolling of all previous exceptions in the stack.

## DX Improvements
- Added `schedule_timezone` property to `config/app.php`.
- Updated theme scaffold's README.md to reflect the use of Vite in the generated themes.
- Added `test` alias for the `winter:test` command.
- Added support for customizing the Vite build directory.
- Added support for `ReactJS` in Vite & Mix compiled asset packages.
- Improved support for [Model Factories](https://laravel.com/docs/9.x/eloquent-factories).

## API Changes
- Added support for an array of names to use for the `postbackHandlerName` in the Table widget.
- Removed the `config:cache` command as it wasn't improving our performance and didn't fully work with Winter's flexible configuration system.

## Bug Fixes
- Removed redundant backend route.
- Fixed issues where TagList & Repeater FormWidgets were not able to save an empty value.
- Fixed issue where TagList could return an object in array mode.
- Fixed using Vite packages when they are explicitly ignored / excluded from the project's `package.json`.
- Improved support for `winter:mirror` on Windows
- Using the `{% flash %}` tag in Twig will now properly purge the FlashBag after it has been read.
- Improved support for plugins attempting to access the database before it's fully ready to go.
- Fixed suport for hex colors with alpha values.
- Fixed infinite loop that occurrs when the configured database exists but the tables don't exist yet and / or they've been bought out.
- Fixed support for array callables as dynamic methods.
- Event listeners bound to events with `bindEventOnce()` now properly unbind after execution, even if the event is a halting event.
- Fixed Syntax Error in CAST Statement for Postgres attachment.

## Security Improvements
- Added AllowList functionality to the Twig security policy.

## Translation Improvements
- Improved Russian translations.

## Performance Improvements
-

## Community Improvements
-

## Dependencies
- Added support for PHP 8.4
- Dropped support for PHP 8.0, PHP 8.1 is now the minimum requirement.