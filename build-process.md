# Winter CMS Build Process

Winter CMS does not use semantic versioning. The idea of Winter CMS is to be an evergreen solution that avoids breaking changes in builds as much as possible and always requires manual confirmation before updating to a build where a breaking change is made.

The code base for the project lives in two main repositories: https://github.com/wintercms/winter and https://github.com/wintercms/library. The project is available for installation through a web installer fed by the marketplace server (https://wintercms.com) and by using Composer. When using Composer, the wintercms/winter repo is split into three separate repos for inclusion by composer: wintercms/wn-backend-module, wintercms/wn-system-module, wintercms/wn-cms-module. The wintercms/winter repo is the example of a working Winter CMS project and is where active development happens for the sake of simplicity while the split repos are to make it easier to pick & choose the modules you want to use for your Winter CMS project (NOTE: wintercms/wn-system-module & wintercms/library are the core of what Winter CMS is and are required for wintercms/wn-backend-module, winterrain/cms, and the plugins to function).

The development / build process is the following:

1. Active development is done in the develop branches.
2. Development progress is periodically manually synced from wintercms/winter to the wintercms/*module* repos (meaning that occasionally the composer packages may be out of date with the wintercms/winter repository)
3. When a new build is ready for release, it is tagged on GitHub and pulled in the marketplace server and marked as "Pending". This update will go out to anyone with cms.enableEdgeUpdates set and anyone using composer referencing a version number.
4. After the pending build has been tested and is considered ready for stable release then the tagged commit is merged into the master branches and the marketplace server releases the update to all installations.

## Stable Composer Usage
If you are using Composer and only ever want to receive builds that have been marked as stable then you will have to use the following for your Winter CMS requirements:

```json
"wintercms/storm": "~1.1.2",
"wintercms/system": "dev-master",
"wintercms/backend": "dev-master",
"wintercms/cms": "dev-master",
```