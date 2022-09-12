# Build 1.2.1 - WIP

## UX/UI Improvements
- Made the composer merge plugin less greedy by default, previously it would merge in all plugin composer.json files that existed in your project, now it will only merge in specific plugin paths defined in your project's `composer.json`. Copy [the changes](https://github.com/wintercms/winter/commit/e05a20eddc28b0cb4eb6fa8b048fc319cca467ae) from GitHub in order to apply it to your projects.
- Clicking the label of a `switch` field will now toggle the switch.
- Increased the width of the crop dimension inputs when cropping or resizing an image in the Media widget.

## API Changes
- The `twig.environment.cms` Twig environment is no longer provided as a singleton, instead being generated on each request to `App::make()`. This helps to avoid conflicts when calling the CMS controller multiple times in the same request.
- Added the following model relation events:
    - `model.relation.beforeAdd($relationName, $relatedModel)`
    - `model.relation.afterAdd($relationName, $relatedModel)`
    - `model.relation.beforeRemove($relationName, $relatedModel)`
    - `model.relation.afterRemove($relationName, $relatedModel)`
    - `model.relation.beforeAssociate($relationName, $relatedModel)`
    - `model.relation.afterAssociate($relationName, $relatedModel)`
    - `model.relation.beforeDisassociate($relationName)`
    - `model.relation.afterDisassociate($relationName)`
- The AJAX framework and Snowboard framework now both enforce either a class name dot (`.`) or an ID hash (`#`) to be prefixed to any partials that are to be updated in an AJAX response. This includes any mapped selectors.

## Bug Fixes
- The `winter:test` command now automatically uses the correct bootstrap file for unit testing, irrespective of the `bootstrap` configuration in any plugin or module's `phpunit.xml` file, to assist users migrating their unit tests to Winter 1.2.
- Fixed issue where plugins weren't being correctly sorted by their dependencies when depending on a plugin that registers itself as a replacement which could cause migrations to run in the incorrect order.
- Fixed typo in the MediaManager widget that was preventing SVGs from displaying their previews in the sidebar.
- Fixed issue when attempting to generate a TailwindCSS theme scaffold on a case sensitive file system.
- Fixed mismatching method signature on AutoDatasource->lastModified() that could cause issues when using DatabaseTemplates in v1.2.
- Fixed issue where MorphedByMany relationships would use the wrong class name when building queries.
- Removed an override to the `Input::all()` facade method, which prevented files from being included in the result, breaking previous behaviour.
- Removed an extra `0` that was left over in `numberrange` filter partials.

## Security Improvements
-

## Translation Improvements
- Fixed a misnamed language string for the custom editor HTML styles input.

## Performance Improvements
-

## Community Improvements
- The Winter CMS module sub-split is now automated, ensuring that the module repositories are now kept up-to-date with the latest changes soon after they are committed to the main repository.
- The base `System\Tests\Bootstrap\PluginTestCase` class has been signficantly refactored to improve testing in plugins. While it is mostly backwards-compatible, the method `runPluginRefreshCommand` is now deprecated and will be removed in the Winter CMS 1.3 branch. Please use the `instantiatePlugin` method instead if you have overridden the core plugin test case methods.

## Dependencies
-
