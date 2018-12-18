# Build 443:

## UX/UI Improvements:
- Increased the visibility of the close button in modal popups
- Added favicon to backend login page

## API Changes:
- Added `.xml` as a valid default asset file extension
- Added `fit` method for resizing cropped images
- Added `model.relation.beforeAttach`, `model.relation.afterAttach`, `model.relation.beforeDetach`, `model.relation.afterDetach` events
- Added `readOnly` support for `switch` and `checkbox` field types
- Added `getLayout()` method to the CMS Controller
- Added ability for `paneCssClass` to define one class to be applied to all tab panes
- Made automatically inlining brand CSS in email layouts optional

## Bug Fixes:
- Numerous code quality improvements
- Fixed issue with NestedTree on SQL Server: "A column has been specified more than once in the order by list. Columns in the order by list must be unique."
- Added unit tests for the image Resizer class
- Improved backend compatibilty with CloudFlare's RocketLoader
- Fixed input trigger on source field types with multiple selected values

## Translation Improvements:
- Additions to the Russian translation