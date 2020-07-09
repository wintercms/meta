# Build 468 (WIP)

## UX/UI Improvements
-

## API Changes
- The `Encryptable` trait now encrypts "empty" values correctly, such as the number zero and an empty string. The only value that is left unencrypted is a `null` value.

## Bug Fixes
- Unit tests involving authentication are now namespaced to `backend.auth`, to prevent conflicts with other authentication libraries.
- Fixed "use statement with non-compound names has no effect" when attempting to import classes already in the root namespace (like facades) in the CMS PHP code section.

## Security Improvements
-

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
