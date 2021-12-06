# Build 1.1.8 (WIP)

## UX/UI Improvements
-

## API Changes
- Classes implementing the `System\Traits\PropertyContainer` trait to provide dynamic property options for Inspector fields no longer need to have zero (or one optional) parameters in their constructor in order to work correctly. Note that if your constructor requires a value in any property and does not define a default, this will still fail, so ideally you should still use a class specifically set up for handling Inspector properties.
- Added `| md_line` Twig filter to make use of the `Markdown::parseLine()` method in Twig templates.

## Bug Fixes
- Integers can now be used as values for options provided to the Inspector `set` field.
- Fixed issue with list of available encodings for importing where ISO 8859-9 was incorrectly referenced as ISO 8859-0.
- Fixed issue that could occur when running console commands on a project that had replaced plugins and their replacing plugins present at the same time.

## Security Improvements
-

## Translation Improvements
- Improved Latvian translation.
- Improved Ukrainian translation.

## Performance Improvements
-

## Community Improvements
-

## Dependencies
- Laravel 6.x LTS does not support PHP 8.1 so Winter has limited the supported PHP versions to PHP 7.2.9 -> PHP 8.0.*. PHP 8.1 support will come with Winter 1.2 using Laravel 9.x LTS in January 2022.
