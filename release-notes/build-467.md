# Build 467 (WIP)

## UX/UI Improvements
- Added docblocks to the controller scaffolding.
- Added support for decompiling nested compiled asset files when `cms.decompileBackendAssets` is enabled.
- Improved error handling for failed fileuploads

## API Changes
-

## Bug Fixes
- Fixed bug introduced in 466 where `:number` stopped working in transChoice translation strings.
- Fixed bug introduced in 466 where it was impossible to upload images to the Media Library while on a page that included the AssetList widget.
- Fixed bug introduced in 466 where plugin dependencies wouldn't be loaded all of the time.
- Fixed bug where belongsToMany relationships with pivot data could not be added to through the RelationController if a custom `order` property was set on the relationship definition.
- Fixed empty tags being stripped in RichEditor (Froala) widget.
- Fixed bug where a field with `@context` in the name would completely break forms if it also utilized the `dependsOn` API other fields.
- Fixed bug introduced in 466 where backend throttle records were no longer recording the IP address correctly of authentication attempts.
- Fixed visual glitch on Inspector autocomplete dropdown fields

## Security Improvements
- Fixed security issue where content pasted into the Froala richeditor wasn't properly sanitized exposing users to self-XSS attacks from malicious websites when copying & pasting content into the editor.

## Translation Improvements
- Improved the Polish translation.

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
