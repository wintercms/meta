# Build 465 (WIP):

## UX/UI Improvements:
- The Event Log list now shows the entire first line of a logged error message, up to 500 characters maximum, in order to provide more context of errors in the list.
- When searching for plugins to install in the backend plugin management screen author names are now included in the search results.
- A consistent cross browser focus ring style is now utilized in the backend.
- Fixed a small typo when using number range filters with no value provided for the minimum.
- Removed excess space from tab titles when hovering over them.
- Added styling to distinguish a disabled unchecked checkbox from a enabled unchecked checkbox.
- Added ability to middle mouse click on list rows to open them in a new tab.
- Added new `style` attribute for repeater widgets, which controls repeater item behaviour. Allows items to be expanded or collapsed on load, or allows a repeater to act as an "accordion" widget.

## API Changes:
- Type hint for `registerSchedule` method in `PluginBase` updated to correctly hint the `Illuminate\Console\Scheduling\Schedule` object that is passed to it.
- Added `exception.beforeReport` and `exception.report` events
- `cms.backendForceSecure` no longer supports the value of `null` (where it would be considered the inverse of `app.debug`) as this resulted in confusion when disabling debug mode while the application was behind a proxy causing an infinite loop. Ultimately it's the server's responsibility to handle forcing HTTPS.

## Bug Fixes:
- Fixed issue with the `queueOn` and `laterOn` methods of the `Mail` facade throwing an invalid argument exception due to queue name string being defined where the queue manager is meant to be defined. The queue name is now injected into the `Mailable` object that is created, and the default queue manager is used instead.
- Implemented another fix for the temporary monkey patched LESS compilation to support PHP 7.4 until the Laravel 6 upgrade is completed.
- Fixed a bug where attempting to set a simple value on a BelongsToMany relationship as a collection would produce a collection wrapped in an array instead of an array of values which would confuse the `sync()` command.
- Fixed an issue with composer.json which could cause some installations to load a version of Laravel newer than actually supported.
- Fixed issue where un-elevated plugins weren't being loaded on any routes starting with /combine (should have been /combine/)
- Fixed a change in default behavior where a recent update to Dropzone.js (used for uploading files) added a timeout property that defaults to 30 seconds. Timeout has been set to 0 (infinite) to retain the previous behaviour of no timeout utilized on file uploads.

## Security Improvements
-

## Translation Improvements:
- Improved Slovakian translation.
- Improved French translation.

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-
