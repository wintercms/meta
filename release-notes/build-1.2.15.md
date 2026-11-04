# Build 1.2.15 (WIP)

## UX/UI Improvements
- Added "select all records matching this query" to list bulk actions, so an action can be applied to every record matching the current filters instead of only the records on the current page.
- Added an optional tree display with expand / collapse to the `relation` form widget for related models using the nested tree trait.
- Updated the Winter logos and routed the backend's colours through CSS variables, so a skin or plugin can retheme the backend from a single block of tokens.
- Record navigation on backend forms can now follow a named list other than the controller's primary one, which makes it available on screens whose primary list is deliberately a subset.
- Compacted the icon picker and fixed its behaviour inside dynamic forms.
- Option icons are now shown in `select2` dropdowns that accept custom values.
- Added accessible names to the datepicker and single fileupload form widgets.

## API Changes
- **Safe mode has been removed.** `cms.enableSafeMode` is no longer read and `Cms\Helpers\Cms::safeModeEnabled()` is gone, so the PHP code section of CMS pages, layouts and partials is always available. Editing one of those templates already requires a permission that grants direct access to the theme's files, so safe mode refused a thing its holder could do by other means. A `config/cms.php` that still carries `enableSafeMode` is harmless; the value is simply not read.
- **Theme import is no longer disabled in production.** Safe mode gated the import form and handler, and because it defaulted to the inverse of `app.debug`, that gate was on for every install that never set the config value. Importing a theme writes theme files, which is what `cms.manage_themes` is for, so both import handlers now require that permission rather than inheriting the controller's wider check.
- **Theme templates and module / plugin views are no longer sandboxed, and mail content now is.** `twig.environment` (the `.htm` view engine, so module and plugin views) and `twig.environment.cms` (theme templates) drop the Twig sandbox. `twig.environment.mailer` keeps it, rebuilt as an allowlist in `System\Twig\SandboxPolicy`. `System\Twig\SecurityPolicy`, `System\Twig\SecurityPolicy\SafeCollection`, `System\Twig\SecurityPolicy\SafePaginator`, `System\Twig\Node\GetAttrNode` and `System\Twig\GetAttrAdjuster` are removed.
- **Mail templates and mail views are rendered against that allowlist, including mail views a plugin ships.** A mail template or view that used the `str_*`, `array_*`, `url_*`, `html_*` or `form_*` filter families, or `{% include %}` or `{% extends %}`, now throws — prepare the value in PHP and pass it into the template as data. Reading data off a value that was passed in is allowed, calling behaviour on it is not, and a model exposes only what its own `$hidden` / `$visible` rules let out, so `{{ user.email }}` renders while `{{ user.fullName }}` and `{{ user.attributes }}` do not.
- `MarkupManager::makeSandboxedTwigEnvironment()` is how a plugin asks for the same sandbox for templates its own users edit. It takes an array of additions to the baseline keyed by `tags`, `filters`, `functions`, `tests` and `methods`; any other key throws rather than being ignored.
- `e()` is no longer overridden by Winter, so Laravel's helper applies again: it double-encodes by default, returns a backed enum's value instead of raising, and resolves a `DeferringDisplayableValue`. The case to check is a widget that escapes a value in PHP and escapes it again in its template — that was a no-op before and now applies a second layer, so drop one of the two or pass `e($value, false)` at that call site.
- The asset combiner now holds the list of files it is asked to compile to the same roots it already holds `@import` and `=include` to, plus the local path the calling code declared the list relative to. An entry outside them is dropped and logged by name. The `resources` component also refuses a property value containing a parent reference. Cache entries written before this release are served as they were, so clear the combiner cache if you want the old URLs gone.
- `node_modules` is now an allowed import root for LESS and SCSS assets.
- `Backend\Traits\InspectableContainer::onInspectableGetOptions()` resolves a class name against a new `protected listInspectableClasses()`, which answers from the registered components and the registered report widgets. A controller publishing an inspectable class of its own needs to add it to that list.
- A `relation` configured as `readOnly` now refuses its write handlers, where before `readOnly` was consulted only while rendering the controls that reach them.
- `Attach\File::output()` and `outputThumb()` accept only `inline` or `attachment` as a disposition and raise `InvalidArgumentException` for anything else. An attachment whose recorded content type is HTML, SVG or XML is served as a download rather than in place; images and PDFs are unchanged.
- A thumbnail requested with an extension the resizer cannot encode is now named `.png`, as is a thumbnail taken from a source file whose own extension is not an image format. Cached thumbnails of that kind are orphaned and regenerate under the new name.

## Bug Fixes
- Fixed a `nestedform` field crashing the whole form when it has no value and one of its sub-field names collides with a model attribute.
- A backend confirm dialog now accepts Enter as soon as it opens, where before the keypress closed the dialog, dropped the request and left its promise unresolved.
- Fixed the `checkboxlist` form field losing its indent.
- Filter widgets on a model relation no longer trigger the form's change monitor.
- Added the `cache_locks` table that Laravel's `database` cache driver keeps its locks in, so `Cache::lock()` and scheduled tasks using `withoutOverlapping()` or `onOneServer()` work on that driver.
- Mix and Vite packages belonging to a symlinked plugin now register with the asset `PackageManager` instead of being dropped.
- A signed-in backend user who opens or posts to the password restore form is now redirected to the backend, so the form's behaviour no longer depends on whether a session is present.
- A CSS asset that `@import`s a remote stylesheet now leaves the `@import` in the combined output for the browser to resolve, instead of inlining the fetched response.
- `Ini::parse()` returns a value as written instead of substituting the value of any PHP constant a token happens to name, and an unparseable settings section becomes the section parser's error attribute rather than silently emptying the document.
- `Html::clean()` now removes only the attribute it means to remove: a tag is no longer truncated at a `>` inside an attribute value, attributes following a removed one are kept, and an attribute whose name merely begins with a removed name is left alone.
- Fixed the in-memory query cache hashing a query before its selected columns were applied, so two queries differing only by their columns no longer share an entry.
- Fixed the provider-loading retry not rebuilding the package manifest, which booted the application with no discovered providers and swallowed the original exception.
- Fixed `hasRelation()` being the first relation call on a model leaving `getDefinedRelations()` returning only that one relation.

## Security Improvements
- Hardened backend controller URL handling.
- Narrowed the Twig sandbox to the templates a developer did not write, and rebuilt the policy that applies to them.
- Confined the Media Manager and the image resizer to their configured roots.
- Applied the relation, list and reorder behaviours' own record scoping to their write paths.
- Tightened report widget selection and dashboard layout rendering.
- Improved escaping of stored values rendered by backend widgets and settings pages.
- Tightened the asset combiner's import confinement, entry list and error output.
- Hardened per-item permission checks in the Settings controller.
- Hardened the CMS asset list's handling of theme asset names.
- Hardened the handling of the core build identifier.
- Hardened the `winter:util git pull` utility.
- Hardened the backend sign-in session.
- Hardened how the backend serves stored file attachments.
- Constrained generated thumbnail file names.
- Narrowed the request paths the system module treats as privileged.
- Improved the removal of unsafe attributes in `Html::clean()`.
- Hardened the project's own CI workflows and code style utilities.

## Translation Improvements
- Improved French translations.
- Improved Italian translations.

## Performance Improvements
- Model relations defined as methods are resolved once per class instead of on every check.
- A cached Halcyon lookup for a template that does not exist is now stored as a cache hit, so rendering a component partial no longer asks the datasource for the missing override on every request.

## Community Improvements
- Reduced the core PHP test suite's runtime on CI by roughly 6x. `System\Tests\Concerns\MigratesDatabaseOnce` is available to plugin suites that want the same, `winter:test -p <plugin>` now runs plugin suites at the reduced hashing cost, and the per-base-class cost of adding a test is documented in `modules/system/tests/README.md`.
- Configured `composer audit` to ignore Laravel framework advisories, which Winter 1.2's Laravel 9 requirement cannot act on.
- Expanded `AGENTS.md` with the backend styling iteration loop, the traps of developing against a symlinked plugin, and the rule against hand editing compiled CSS.

## Dependencies
- Bump minimum version of `assetic/framework` to `v3.2.3`.
- Upgraded `enshrined/svg-sanitize` to `~1.0`.
- Added an explicit requirement on `league/commonmark` of `^2.10.2`.
