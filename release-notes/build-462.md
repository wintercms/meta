# Build 462:

## UX/UI Improvements:
- Documented `session.http_only` config property in the default `config/session.php`

## API Changes:
- Event logs are now double-encoded for HTML characters before being displayed as both HTML and text in the event log viewer. This allows encoded HTML entities to be parsed and displayed correctly in the HTML view, but displayed exactly as entered in the text view.

## Bug Fixes:
- Fixed janky behaviour with the javascript sortable plugin when sorting items on a scrollable container (affected RainLab.Sitemap, RainLab.Pages, Menus, etc).
- Fixed issue where linked data in singular relation controller (hasOne or belongsTo) would remain populated in the relation fields even after unlinking or deleting the linked record.

## Dependencies
- Changed Laravel dependency to require 5.5.40 as a minimum due to the breaking change Laravel made in that version, some composer installs were not recognizing anything newer than 5.5.38 so this bump makes it more obvious that a stale composer is the issue.
