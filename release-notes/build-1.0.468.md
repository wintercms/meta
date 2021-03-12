# Build 1.0.468

## UX/UI Improvements
- Added new Paragraph Formats option to the Editor Settings page, which allows you to control the available tags in the Paragraph Formats button.

## API Changes
- The `Encryptable` trait now encrypts "empty" values correctly, such as the number zero and an empty string. The only value that is left unencrypted is a `null` value.
- Fixed docblocks in the `Winter\Rain\Network\Http` class that referred to the `$options` property as an `array` instead of the `callable` that is actually used

## Bug Fixes
- Unit tests involving authentication are now namespaced to `backend.auth`, to prevent conflicts with other authentication libraries.
- Fixed "use statement with non-compound names has no effect" when attempting to import classes already in the root namespace (like facades) in the CMS PHP code section.
- Fixed a bug where the text entry of a `taglist` field would remain after the tag has been created.
- Resolved an issue where PHP `max_input_vars` limits would prevent "group" filters from working if they contained more options than `max_input_vars` would allow.
- Fixed support for `ignoreTimezone` in `date` and `daterange` filter scope types.
- Fixed issue with Arabic translation in the backend where Indic numerals were being used instead of Arabic numerals for the `datepicker` FormWidget which was confusing the serverside processing of date values.
- Fixed issue where an incorrect `<textarea>` tag definition broke the popup editor for `stringList` and `text` type fields in the Inspector.

## Security Improvements
- Improved validation of encrypted cookies by locking cookie values to the cookie they were created for. See [the security advisory](https://github.com/wintercms/winter/security/advisories/GHSA-55mm-5399-7r63) for more information.

## Translation Improvements
- Improved French translation.

## Community Improvements
- Added note in `config/cms.php` for handling URL generation for uploaded files when using Winter in a subfolder installation.