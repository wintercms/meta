# OctoberCMS Build Process

OctoberCMS does not use semantic versioning. The idea of OctoberCMS is to be an evergreen solution that avoids breaking changes in builds as much as possible and always requires manual confirmation before updating to a build where a breaking change is made.

The code base for the project lives in two main repositories: https://github.com/octobercms/october and https://github.com/octobercms/library. The project is available for installation through a web installer fed by the marketplace server (https://octobercms.com) and by using Composer. When using Composer, the octobercms/october repo is split into three separate repos for inclusion by composer: octoberrain/backend, octoberrain/system, octoberrain/cms. The octobercms/october repo is the example of a working OctoberCMS project and is where active development happens for the sake of simplicity while the split repos are to make it easier to pick & choose the modules you want to use for your OctoberCMS project (NOTE: octoberrain/system & octobercms/library are the core of what OctoberCMS is and are required for octoberrain/backend, octoberrain/cms, and the plugins to function).

The development / build process is the following:

1. Active development is done in the develop branches.
2. Development progress is periodically manually synced from octobercms/october to the octoberrain/* repos (meaning that occasionally the composer packages may be out of date with the octobercms/october repository)
3. When a new build is ready for release, it is tagged on GitHub and pulled in the marketplace server and marked as "Pending". This update will go out to anyone with cms.enableEdgeUpdates set and anyone using composer referencing a version number.
4. After the pending build has been tested and is considered ready for stable release then the tagged commit is merged into the master branches and the marketplace server releases the update to all installations.

## Stable Composer Usage
If you are using Composer and only ever want to receive builds that have been marked as stable then you will have to use the following for your OctoberCMS requirements:

```json
"october/rain": "dev-master as 1.0",
"october/system": "dev-master",
"october/backend": "dev-master",
"october/cms": "dev-master",
```