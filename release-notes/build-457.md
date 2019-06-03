# Build 457 (WIP):

## UX/UI Improvements:
-

## API Changes:
- The `October\Rain\Database\Attach\File` model's `getPath()` now defines an optional `$fileName` parameter, any custom classes that extend this method must have their method signatures updated to match this change.
- The `getDisk()` method has been added to the `October\Rain\Database\Attach\File` model which enables running all storage related commands on the File's actual storage disk instead of the default storage disk.

## Bug Fixes:
-

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