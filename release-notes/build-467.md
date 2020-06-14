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