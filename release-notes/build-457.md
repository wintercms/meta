# Build 457 (WIP):

## UX/UI Improvements:
- Now utilizing the selected `secondaryColor` brand setting for the border color on selected items in the Treeview control (pages list)
- Added support for `cms.databaseTemplates` to the `october:env` command

## API Changes:
- The `October\Rain\Database\Attach\File` model's `getPath()` now defines an optional `$fileName` parameter, any custom classes that extend this method must have their method signatures updated to match this change.
- The `getDisk()` method has been added to the `October\Rain\Database\Attach\File` model which enables running all storage related commands on the File's actual storage disk instead of the default storage disk.
- Added new `Backend\Traits\PreferenceMaker` trait modelled after the `SessionMaker` trait that stores minor user preference changes (such as backend list configurations) in the user's preferences.

## Bug Fixes:
- Fixed support for JS plugins extending the RichEditor
- Improved the Halcyon `addDynamicProperty` test
- Fixed issue where CMS Meta information wasn't populating correctly (breaking menus in RainLab.Pages)
- Fixed issue where mainMenu counter's being set to `false` didn't properly disable them fully from displaying
- Improved reliability of `jsonable` properties in models under conditions where they might be double de/encoded for one reason or another
- Fixed broken path to the video thumbnail in the MediaManager widget
- Fixed issue when attempting to interact with CMS assets in the backend caused by the recent addition of the `databaseTemplates` functionality

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
- When using Cloud storage drivers (ex. AWS or Rackspace) for `File`s that are marked as protected, the `Backend\Controllers\Files` controller's `getDownloadUrl()` and `getThumbUrl()` methods now return temporary URLs to the actual asset instead of a URL that proxies the entire asset through the framework to the browser. The amount of time the temporary URL is valid for is configurable by setting `cms.storage.uploads.temporaryUrlTTL` to a value in seconds (default 3600, an hour). This should dramatically improve performance of protected files that are located in storage drives that support the `getTemporaryUrl()` method - and it is recommended that if you heavily utilize that feature that you utilize a storage drive that supports that method.

## Community Improvements:
-

## Dependencies
- Added inline_style and inline_class Froala plugins into the base Froala build