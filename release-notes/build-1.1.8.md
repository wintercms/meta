# Build 1.1.8 (WIP)

## UX/UI Improvements
- The `winter:down` command now requires a user to explicitly confirm the action by typing `DELETE` in their CLI.
- The `plugin:remove` command now requires a user to explicitly confirm the action by typing the plugin code in their CLI.

## API Changes
- Classes implementing the `System\Traits\PropertyContainer` trait to provide dynamic property options for Inspector fields no longer need to have zero (or one optional) parameters in their constructor in order to work correctly. Note that if your constructor requires a value in any property and does not define a default, this will still fail, so ideally you should still use a class specifically set up for handling Inspector properties.
- Added `| md_line` Twig filter to make use of the `Markdown::parseLine()` method in Twig templates.
- Replaced `Winter\Storm\Auth\AuthException` with `Winter\Storm\Auth\AuthenticationException`, added `Winter\Storm\Auth\AuthorizationException`.
- The `plugin:remove` command now provides a `--no-rollback` option which disables the rolling back of database migrations for a plugin when it is being removed, allowing the plugin data to be retained.

## Bug Fixes
- Integers can now be used as values for options provided to the Inspector `set` field.
- Fixed issue with list of available encodings for importing where ISO 8859-9 was incorrectly referenced as ISO 8859-0.
- Fixed issue that could occur when running console commands on a project that had replaced plugins and their replacing plugins present at the same time.
- Fixed incorrect exception message when attempting to impersonate a user without authorization.
- Fixed color picker widget not allowing empty values.
- Fixed color picker widget showing misleading mouse cursors in read-only mode.
- Fixed color picker widget not triggering dependent fields on change.
- Fixed issue where attempting to render a theme without a database present would fail because the AssetMaker trait was attempting to get the system build information from the database even though the DB wasn't present.

## Security Improvements
-

## Translation Improvements
- Improved Latvian translation.
- Improved Ukrainian translation.
- Improved French translation.

## Performance Improvements
-

## Community Improvements
-

## Dependencies
- Laravel 6.x LTS does not support PHP 8.1 so Winter has limited the supported PHP versions to PHP 7.2.9 -> PHP 8.0.*. PHP 8.1 support will come with Winter 1.2 using Laravel 9.x LTS in January 2022.
