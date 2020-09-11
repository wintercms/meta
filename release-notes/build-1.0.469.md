# Build 1.0.469

## API Changes
- `.svg` has been removed from the default list of allowed extensions for uploading for security reasons, will be re-added in Build 1.1.1 alongside sanitization to protect against XSS attacks. Use `storage.media.defaultExtensions` to override the default list of allowed extensions in order to re-add support for it at your own risk.
- `$fileName` was removed as a parameter for the `October\Rain\Halcyon\Builder->delete()` method as it wasn't actually being used internally and had no effect.
- Partials included via `$this->renderPartial()`, `{% partial 'path/to/partial' %}`, and `{% include 'path/to/partial` %} now properly block all extensions other than `.htm` by default.
- Attempting to load & render partials from outside of the theme using the CMS Twig engine will no longer work (note, this was never officially supported, it was a bug that it ever worked in the first place). If you are trying to render Twig from outside the theme you should always use the System Twig engine instead of the CMS one by calling `\Twig::parse($templateContents, $templateVars);`)

## Bug Fixes
- Fixed issue where cookies that were generated at some point between pre-Laravel 5.5.* cookie security fix and the latest cookie security fixes in Build 1.0.468 could fail to be processed correctly.
- Fixed an issue where some SystemExceptions include unfiltered user input in the response to the browser, which would cause security researchers to think that they've found a XSS vulnerability which would then take resources to explain how it wasn't exploitable by just stripping any potential XSS from SystemException messages.

## Security Improvements
- Fixed issue where the FileDatasource could be abused to load files outside of the intended location.
- Fixed issue where the Twig sandbox could be escaped allowing users with access to Twig templates to define and run PHP code.

## Community Improvements
- October has moved to a slightly different versioning scheme, major changes such as Laravel framework upgrades will now be indicated by the "minor" version number, and the build / patch number will reset on every increment of the minor version number. October builds from initial conception to Laravel 5.5 EOL will be the v1.0.319 to v1.0.469 range, and the Laravel 6 upgrade will be v1.1.0. EOL branches will not be supported with bug fixes or feature additions, but will continue to have security issues IN OCTOBER CODE ONLY (i.e. security fixes for dependencies will not be included) fixed as they are reported to the core team through our Security Policy.