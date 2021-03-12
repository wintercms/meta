# Build 1.0.470

## API Changes
- The `Winter\Rain\Database\Attach\File` model now uses "fillable" attributes as opposed to "guarded" attributes to control mass assignment. If you extend the `File` (or the main `System\Models\File`) model to provide additional fields, you must now copy the "fillable" attributes to your extension and add any additional fields to this definition (backported from 1.1.0)

## Bug Fixes
- Temporarily fixed an issue with existing code-bases that abuse the Twig engine by loading template files in unsupported ways (`.js` / `.svg` files rendered as partials through `{% partial %}`, `{% include %}`, or `$this->renderPartial()`). NOTE: This hotfix will not be available in Build 1.1.x so existing code still needs to be fixed to not use those unsupported file types.
- Fixed an issue introduced in Build 1.0.469 where plain Twig templates couldn't be loaded through the `{% include 'path' %}` or `{{ source(path) }}` Twig functions
- Fixed issue introduced in a security update to Laravel 5.5 where models with guarded properties were failing to allow attributes that don't have a corresponding column to be processed in events (for example, the "data" attribute in the File model). (backported from 1.1.1)

## Security Improvements
- Tightened up the default permissions granted to the "Publisher" system role out of the box (backported from 1.1.1).
- Locked down the Twig sandbox even more to prevent allowing users with access to Twig templates from defining and running PHP code (backported from 1.1.1).