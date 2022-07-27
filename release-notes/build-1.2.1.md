# Build 1.2.1 - WIP

## UX/UI Improvements
- Made the composer merge plugin less greedy by default, previously it would merge in all plugin composer.json files that existed in your project, now it will only merge in specific plugin paths defined in your project's `composer.json`. Copy [the changes](https://github.com/wintercms/winter/commit/e05a20eddc28b0cb4eb6fa8b048fc319cca467ae) from GitHub in order to apply it to your projects.

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

## Bug Fixes
- The `winter:test` command now automatically uses the correct bootstrap file for unit testing, irrespective of the `bootstrap` configuration in any plugin or module's `phpunit.xml` file, to assist users migrating their unit tests to Winter 1.2.
- Fixed issue where plugins weren't being correctly sorted by their dependencies when depending on a plugin that registers itself as a replacement which could cause migrations to run in the incorrect order.
- Fixed typo in the MediaManager widget that was preventing SVGs from displaying their previews in the sidebar.
- Fixed issue when attempting to generate a TailwindCSS theme scaffold on a case sensitive file system.
- Fixed mismatching method signature on AutoDatasource->lastModified() that could cause issues when using DatabaseTemplates in v1.2.
- Fixed issue where MorphedByMany relationships would use the wrong class name when building queries.

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
