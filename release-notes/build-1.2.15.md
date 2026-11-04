# Build 1.2.15 (WIP)

## UX/UI Improvements
- Added expand / collapse controls to the `Relation` FormWidget.
- Added a "select all records matching this query" option to list bulk actions, enabled by default on newly scaffolded controllers.
- Record navigation now follows a named list and can be overridden by the controller.
- Refreshed the Winter logos and exposed the backend brand colours as CSS variables.
- Option icons are now shown in `select2` dropdowns that allow custom values.
- Compacted the icon picker and fixed its behaviour inside dynamic forms.
- Confirm dialogs now accept input as soon as they open.
- Added accessible names to the datepicker and single file upload widgets.

## Bug Fixes
- Fixed the indentation of the `checkboxlist` form field.
- Fixed `input.monitor.js` for relation filters.
- Fixed `NestedForm` falling back to the parent model when empty.
- Added the `cache_locks` table required by the database cache driver.
- Added `node_modules` as an allowed asset import root.
- Fixed support for symlinked plugins in the asset `PackageManager`.
- Authenticated users are now redirected away from the password restore form.

## Security Improvements
- Hardened backend controller URL handling.
- Confined the Media Manager and the image resizer to their configured roots.
- Applied the relation, list and reorder behaviours' own record scoping to their write paths.
- Tightened report widget selection and dashboard layout rendering.
- Improved escaping of stored values rendered by backend widgets and settings pages.
- Tightened the asset combiner's import confinement and error output.
- Hardened per-item permission checks in the Settings controller.
- Hardened the project's own code style utilities.

## Translation Improvements
- Improved French translations.
- Improved Italian translations.

## Community Improvements
- Reduced the runtime of the PHP test suite by roughly six times on CI, and added the `MigratesDatabaseOnce` trait that plugin test suites can opt into for the same benefit.
- Expanded `AGENTS.md` with guidance on the asset pipelines, symlinked plugin development, backend styling iteration, and running `phpcs` locally before pushing.
- `composer audit` now ignores advisories that do not apply to the supported Laravel version.
