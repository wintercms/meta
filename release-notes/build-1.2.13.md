# Build 1.2.13

## UX/UI Improvements
- Added support for inline drag-and-drop sorting for lists and relations.
- Renamed `CMS` to `Theme Editor` in the backend menu.
- Minimized flash of unstyled content when switching between multiple codeeditor instances.
- Restored AceEditor keyboard shortcuts of (Ctrl|Cmd+Shift+D) for duplicating the current selection & (Ctrl|Cmd+Shift+F) for full screen mode
- Fixed support for dragging content (i.e. text links, partials, content files) into the CodeEditor field.
- Fixed highlighting paired tokens in Twig mode by bringing in the full HTML mode processing into Twig mode.
- Fixed issues caused when swapping between multiple editor instances where editor state (position, selection, folding, history) wasn't being retained across editor disposal.
- Fixed default "Twilight" theme to more closely match the original Twilight theme used by AceEditor.
- Improved permission checking to allow users with one of `cms.manage_pages`, `cms.manage_layouts`, or `cms.manage_partials` to still be able to view the list of partials.
- Improved UX of the Permission Editor formwidget and included better descriptions of riskier permissions.
- Added basic viewer for event log details.
- Improved handling of errors when rendering default form controller views.

## DX Improvements
- Added PHP 8.5 to the CI test matrix and improved PHP 8.5 compatibility.
- Added `AGENTS.MD` to `wintercms/winter` to improve the experience of using AI agents to work on the core.

## API Changes
- Added support for the `schema:dump` command.
- Enhanced `HasSortableRelations` for the new inline drag-and-drop sorting provided by the `RelationController`.

## Bug Fixes
- Improved handling of terminal signals on Windows.
- Brought `attributesToArray()` more in-line with Laravel eliminating several bugs related to using the `$casts` property in Winter `Model` classes.
- Improved validation of Theme directory names.
- Added support for returning Vite assets in their correct group (i.e. styles vs scripts).
- Fixed TypeError when removing a non-existent plugin.
- Fix infinite loop in form widget with circular dependsOn declarations.
- Improved support for PHP 8.4 & 8.5.
- Fixed issue where Monaco editor was triggering false dirty state on forms.

## Security Improvements
- Fixed issue where environment variables could be leaked through the parsing of INI configuration values (CVE-2026-25125).
- Improved LESS import security functionality.
- Improved escaping of BrandSetting & EditorSetting custom CSS settings.
- Fixed potential SQL injection with the backend Filter widgets.
- Fixed potential user account bypasses by moving the My Account page to a dedicated controller.
- Closed bypasses making use of the legacy AJAX postback handler.
- Hardened user management by moving more authorization checks directly into the User model itself to prevent modifications at the lowest level.
- Improved permission checking in the CMS / Theme Editor backend page.
- Ensured FileUpload formwidget only ever looks at related file records.
- Hardened Twig Security Policy / Safe Mode logic.

## Translation Improvements
- Improved Ukranian translations.

## Performance Improvements
- Improved performance of retrieving HasMany relationships.

## Community Improvements
- Added [Damien Mathieu](https://github.com/damsfx) as a core maintainer.

## Dependencies
- Upgraded `nikic/php-parser` to `^5.7`
