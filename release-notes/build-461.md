# Build 461:

## UX/UI Improvements:
- Set the CMS `codeeditor` field to readonly and added a warning message above it when safemode is enabled.

## API Changes:
- Bumped minimum required version of PHP from 7.0 to 7.0.8 to enable support for PHP 7.4.
- Added support for the `customViewPath` configuration property in the RelationController when rendering lists to be able to override the partials used for rendering the `Lists` widget.
- Using the `ImportExportController`'s `useList` property will now pass the list header values through the `backend.list.overrideHeaderValue` event just like a regular list would.
- ApplicationException are no longer logged if unhandled (they're meant as more of a validation / sanity check exception. SystemExceptions are logged instead.
- All Artisan commands that are unusable in October (typically because they rely on a "Laravel" project structure) are no longer registered and thus no longer made available. Full list of removed commands here: [octobercms/library#447](https://github.com/octobercms/library/pull/447)
- Added static method `Cms\Helpers\Cms::safeModeEnabled()` to check if safe mode is enabled.
- Add support for lazy loading backend form tabs with the `lazy` configuration property that takes an array of tab names to apply lazy loading to.

## Bug Fixes:
- Fixed scrolling issue in the MediaManager that would occur on some browsers causing scrolled content to no longer become visible erratically.
- Added smoother support for old serialized cookie data to retain sessions during the upgrade process.
- Fixed bug where repeaters with names that started with names of other repeaters on the same page would get confused by each other.

## Translation Improvements:
- Added Slovenian translation

## Community Improvements:
- Switched to using Discord instead of Slack: https://discord.gg/gEKgwSZ
- Launched Premium Support: https://octobercms.com/premium-support

## Dependencies
- Minimum PHP version bumped from 7.0.0 to 7.0.8
- Support for PHP 7.4 added