# Build 462 (WIP):

## UX/UI Improvements:
-

## API Changes:
- Event logs are now double-encoded for HTML characters before being displayed as both HTML and text in the event log viewer. This allows encoded HTML entities to be parsed and displayed correctly in the HTML view, but displayed exactly as entered in the text view.

## Bug Fixes:
- Fixed janky behaviour with the javascript sortable plugin when sorting items on a scrollable container.
- Fixed issue where linked data in singular relation controller (hasOne or belongsTo) would remain populated in the relation fields even after unlinking or deleting the linked record.

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-
