# Build 1.0.470

## UX/UI Improvements
-

## API Changes
- The `October\Rain\Database\Attach\File` model now uses "fillable" attributes as opposed to "guarded" attributes to control mass assignment. If you extend the `File` (or the main `System\Models\File`) model to provide additional fields, you must now copy the "fillable" attributes to your extension and add any additional fields to this definition (backported from 1.1.0)

## Bug Fixes
- Temporarily fixed an issue with existing code-bases that abuse the Twig engine by loading template files in unsupported ways (`.js` / `.svg` files rendered as partials through `{% partial %}`, `{% include %}`, or `$this->renderPartial()`). NOTE: This hotfix will not be available in Build 1.1.x so existing code still needs to be fixed to not use those unsupported file types.

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