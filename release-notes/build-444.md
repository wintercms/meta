# Build 444:

## UX/UI Improvements:
- Replaced the PNG flag icons with the flag-icon-css library that uses SVGs and has more flags available.
- Added filters to the backend logging pages (access, theme, event)
- Icons added to the Status dashboard widget
- Icon added to CMS section to see the last modified date of files
- Resize popovers dynamically when the viewport resizes
- Added ability to define icons for tabs
- Added "Apply" & "Clear" buttons to filter popups
- Added support for 'auto' placement of the time picker widget (based on viewport)
- Added ability to install October.Drivers and RainLab.Builder plugins from the october:install command
- Added readOnly support to RecordFinder, Switch, & Relation form widgets
- Improved the visibility of the code editor control buttons
- Collapse folders in the CMS by default
- Changed the number field type to actually use the HTML5 'number' input type
- Added clear search button when the search widget has content in it
- Improve Datatable dropdown UX, now able to type partial options to select them and use arrow keys to navigate the items

## API Changes:
- Added support for registerMailTemplates and registerMailPartials in the Plugin registration file
- Added support for the `placeholder` property in the TagList FormWidget
- Added '@framework.extras.js' and '@framework.extras.css' file specific aliases to the combiner (Previously they were both combined under the 'framework.js' alias which is still available)
- Added translation support to the 'default' form field property
- Added change detection on the relation controller so that dependsOn can be used on relation controller’s containing fields
- Remove unused X-UA-Compatible meta tag from backend layout
- Implemented SoftDeleting of backend users

## Bug Fixes:
- Added a missing content-type header to CSV exports
- Improved table column width handling in Chrome
- Improved compatibility with using CloudFlare performance tools on backend routes
- Fixed z-index conflict for the markdown editor when in full screen mode
- Fixed file upload fields not correctly saving in the relation controller create popup
- Fixed issue where using Ctrl+F would mark the code editor as "dirty"
- Fixed filter popups not displaying when in a popup modal
- Improved relation controller’s handling of VARCHAR keys
- Fixed not being able to delete asset files in the CMS
- Fixed minItems & maxItems support for Repeaters using groups
- Prevent plugins that cannot be instantiated from being loaded (fixes issues with plugins that include reserved words in their namespaces crashing the whole application)
- Improved CSS minification effectiveness

## Security Improvements
- Escape output of various variables displayed in the backend to prevent theoretical XSS attacks
- Prevent access to controllers of disabled plugins

## Translation Improvements:
- Minor improvements to the Slovak translation
- Additions to the Dutch translation

## Dependencies
- jQuery updated from 2.0 to 3.3.1
- jQuery Migrate was added, accessible with the '@jquery.migrate' alias
- Modernizr updated from 2.8.3 to 3.6.0
- Moments.js & Timezone from 2.13.0 to 2.22.0
- Raphaël updated from 2.1.2 to 2.2.7
- Eve.js updated from 0.4.2 to 0.5.4
- jQuery.isotope.js updated from 1.5.26 to 3.0.6