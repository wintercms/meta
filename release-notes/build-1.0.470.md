# Build 1.0.470

## UX/UI Improvements
-

## API Changes
- The `October\Rain\Database\Attach\File` model now uses "fillable" attributes as opposed to "guarded" attributes to control mass assignment. If you extend the `File` (or the main `System\Models\File`) model to provide additional fields, you must now copy the "fillable" attributes to your extension and add any additional fields to this definition (backported from 1.1.0)

## Bug Fixes
-

## Security Improvements
- Tightened up the default permissions granted to the "Publisher" system role out of the box (backported from 1.1.1)

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-