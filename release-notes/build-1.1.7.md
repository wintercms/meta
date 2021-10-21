# Build 1.1.7 (WIP)

## UX/UI Improvements
- You can now define one or more IP addresses that may view the site during maintenance mode via the Maintenance mode Settings screen.
- Console scaffolding commands (i.e. `create:controller`, `create:plugin`, etc) will now list the files that were created during the scaffolding process for clarity.

## API Changes
- Added `$data` as the fourth argument to the `mailer.prepareSend` and `mailer.send` events.
- Added `create:settings {plugin} {settings=Settings}` scaffolding command to generate a Settings model for the provided plugin.

## Bug Fixes
- Fixed issue introduced in v1.0.466 where copying the default RelationController markup to use in a controller-level override of RelationController partials would result in an "undefined index" exception.
- Client language files for child locales (i.e. `en-ca`) will now include fallback strings from their parent locales.
- Fixed an issue with the Markdown Editor in Chrome clipping the editor content if the viewport height is restricted while the widget has "stretch" enabled.
- Fixed `Backed\Helper\Backend::makeCarbon()` to correctly default to the backend timezone set in `cms.backendTimezone`

## Security Improvements
-

## Translation Improvements
- Improved Persian translation.
- Improved Latvian translation.
- Improved Russian translation.
- Improved German translation.

## Performance Improvements
-

## Community Improvements
- Winter CMS can now be accessed via the [Gitpod](https://gitpod.io) service, providing near-instant, fully working copies of Winter CMS for testing and development. Please see https://github.com/wintercms/winter/pull/295 for more information.
- The [Architecture Concepts](https://wintercms.com/docs/architecture/introduction) section has been added to the documentation and provide an higher level overview of Winter CMS and some of the advanced time-saving features available within the project.
- The [Maintainer Guide](https://wintercms.com/docs/architecture/maintainer-guide) has been added to the documentation.

## Dependencies
-
