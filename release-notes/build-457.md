# Build 457:

## UX/UI Improvements:
- Now utilizing the selected `secondaryColor` brand setting for the border color on selected items in the Treeview control (pages list)
- Added support for `cms.databaseTemplates` to the `october:env` command
- Added support for preview mode to the Taglist FormWidget
- Improved the visibility of the code editor buttons in the CMS section by changing their colour to one with more contrast
- Disabled the theme config cache when application is in debug mode
- Improved the styling of the colour picker when `allowEmpty: true`
- Improved screen reader accessibility for tabs and improved keyboard navigation in the backend

## API Changes:
- The `October\Rain\Database\Attach\File` model's `getPath()` now defines an optional `$fileName` parameter, any custom classes that extend this method must have their method signatures updated to match this change.
- The `getDisk()` method has been added to the `October\Rain\Database\Attach\File` model which enables running all storage related commands on the File's actual storage disk instead of the default storage disk.
- Added new `Backend\Traits\PreferenceMaker` trait modelled after the `SessionMaker` trait that stores minor user preference changes (such as backend list configurations) in the user's preferences.
- Added `cms.enableBackendServiceWorkers` (defaulting to false) to allow the use of Service Workers in the backend. They have been disabled by default for security purposes to prevent any frontend Service Workers from leaking into the backend.
- Plugin dependencies defined in the plugin registration class `$require` property are now case insensitive.
- Removed support for the invalid `type: relation` column configuration, previously this would warn that is was invalid in the system log and convert to `type: text` automatically. Recommended replacement is to use whatever type the data actually is and then use the `relation:` property to specify the relationship you want to get the value from.
- Added a `is_countable()` polyfill to the library for PHP < 7.3
- Disabled global jQuery AJAX events by default in favour of just the `framework.js` ones. Previously both would fire leading to conflicts between what parameters jQuery sends vs what the AJAX framework. If access to the jQuery AJAX events is required, pass `ajaxGlobal: true` to the options for `$.request(handler, options)` or add `data-request-ajax-global` for the Data Attributes AJAX API.
- Third parameter `$options` added to `Zip::make()` that passes the options onto `Zip->add()`. In addition, the `includeHidden` option has been added which specifies that all hidden files (dot files) from the source should be included in the final Zip destination.
- Added `maxFilesize` option to the `FileUpload` FormWidget, defaults to the `upload_max_filesize` from the server

## Bug Fixes:
- Fixed support for JS plugins extending the RichEditor
- Improved the Halcyon `addDynamicProperty` test
- Fixed issue where CMS Meta information wasn't populating correctly (breaking menus in RainLab.Pages)
- Fixed issue where mainMenu counter's being set to `false` didn't properly disable them fully from displaying
- Improved reliability of `jsonable` properties in models under conditions where they might be double de/encoded for one reason or another
- Fixed broken path to the video thumbnail in the MediaManager widget
- Fixed issue when attempting to interact with CMS assets in the backend caused by the recent addition of the `databaseTemplates` functionality
- Fixed long standing issue where loading indicators would remain in a loading state when an error or flash message was returned from a response forcing the user to reload the page to get back to a usable state
- Improved error message displayed when using a custom Halcyon model that does not have a `dirName` set
- Fixed issue introduced with 447 when trying to get the thumbnail for private files without specifying any options by using default options when generating thumbnails for private files
- Improved handling for error states in the `RelationController` behavior
- Fixed support for `files: true` as an AJAX framework option in newer browsers
- Fixed support for saving Repeater data in Static Pages when a repeater item is deleted
- Fixed support for custom Select2 options via the AJAX framework, also added new format for custom options to be returned in to preserve their order
- Fixed issue where CMS templates with the same filenames (i.e. a partial and a page both called contact.htm) would be unable to be selected in the list of templates in the CMS section.
- Fixed the centering of no record message in lists when tree mode is enabled.
- Stopped minifying CSS rules inside of parenthesis, fixes issue where calc() rules with pixel values were breaking after being run through the asset combiner.
- Fixed support for `ReportWidgets` using the `objectList` property type for their properties.
- Fixed support for `Auth::id()`, there was a typo in the method that rendered it unusable previously.
- Fixed bug when attempting to sort by the `any_template` (Template) column in the CMS Theme Log. To sort by template, change the list setup to show the "Old Template" and "New Template" columns and sort by those instead.
- Fixed inspector option values not being translated.
- Fixed `DataFeed` support for Postgres
- Fixed minor issues with poorly structured HTML from the `dump()` Twig function

## Security Improvements
- Backend ServiceWorkers have been disabled by default to prevent frontend ones from leaking into the backend unintentionally. See `cms.enableBackendServiceWorkers`

## Translation Improvements:
- Improved the Brazilian Portuguese translation
- Improved the Chinese translation
- Improved the Spanish translation
- Improved the Russian translation

## Performance Improvements:
- When using Cloud storage drivers (ex. AWS or Rackspace) for `File`s that are marked as protected, the `Backend\Controllers\Files` controller's `getDownloadUrl()` and `getThumbUrl()` methods now return temporary URLs to the actual asset instead of a URL that proxies the entire asset through the framework to the browser. The amount of time the temporary URL is valid for is configurable by setting `cms.storage.uploads.temporaryUrlTTL` to a value in seconds (default 3600, an hour). This should dramatically improve performance of protected files that are located in storage drives that support the `getTemporaryUrl()` method - and it is recommended that if you heavily utilize that feature that you utilize a storage drive that supports that method.
- Added support for the Priority Hints API supported in newer browsers for backend core assets and the `{% framework %}` tags

## Community Improvements:
- Various improvements (performance and otherwise) made to the TravisCI integration with the main repos to make contributing to PRs a nicer experience
- Various improvements to the automated testsuite (including a new style checker, the existing code base has been cleaned up to conform to the style checker. It may be made more strict in the future, for now all PRs are required to adhere to it)
- Added documentation for the `theme:sync` command and for the `--relative` option for the `october:mirror` command

## Dependencies
- Added inline_style and inline_class Froala plugins into the base Froala build
- Added polyfill for `:focus-visible` CSS selector to the backend (https://github.com/WICG/focus-visible)
- Added polyfill for `event.key` in JS events to the backend (https://github.com/cvan/keyboardevent-key-polyfill)