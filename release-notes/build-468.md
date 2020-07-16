# Build 468 (WIP)

## UX/UI Improvements
- Added new Paragraph Formats option to the Editor Settings page, which allows you to control the available tags in the Paragraph Formats button.

## API Changes
- The `Encryptable` trait now encrypts "empty" values correctly, such as the number zero and an empty string. The only value that is left unencrypted is a `null` value.

## Bug Fixes
- Unit tests involving authentication are now namespaced to `backend.auth`, to prevent conflicts with other authentication libraries.
- Fixed "use statement with non-compound names has no effect" when attempting to import classes already in the root namespace (like facades) in the CMS PHP code section.
- Fixed a bug where the text entry of a `taglist` field would remain after the tag has been created.

## Security Improvements
-

## Translation Improvements
- Improved French translation.

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
