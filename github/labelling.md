The Winter CMS organisation uses the following system of labels and issue types for managing issues and/or pull requests.

## Issue Types

These are assigned to issues based on the type of issue being reported.

| Issue Type | Description |
| ---------- | ----------- |
| Bug | A reported bug that has been confirmed by the maintainers and is awaiting a fix. |
| Enhancement | A new feature or substantial change that has been accepted by the maintainers for future implementation. |
| Unconfirmed Bug | A reported bug that has not yet been confirmed by the maintainers. |
| Proposal | A proposed enhancement, maintenance or feature. (ie. a pre-pull request discussion) |
| Maintenance | Minor maintenance (ie. bug fix, styling fix, small improvement or language tweak) |
| Discussion | An issue that is used for discussion. This can be for pre-pull requests or if the maintainers are seeking comment. |

> **NOTE:** In general, we recommend using GitHub Discussions for proposals and discussion.

## Labels

Labels can be assigned to issues and pull requests, and summarise the statuses of each. Some labels we intend to only use for a single type of submission.

| Label | Issues? | Pull Requests? | Description |
| ----- | ------- | -------------- | ----------- |
| accepted | Yes | No | Issues that have been accepted by the maintainers for inclusion. Used generally for pre-pull request discussions or proposals. |
| blocked | Yes | Yes | Issues and pull requests that cannot proceed at this point. The reason for this will be found in the issue or PR's comments. |
| duplicate | Yes | No | Issues that are a duplicate of another reported issue. |
| enhancement | No | Yes | Pull requests that implement a new feature or make a substantial change. This is at the determination of the maintainers. |
| hacktoberfest | No | Yes | The pull request is requested by the submitter to be included in [Hacktoberfest](https://hacktoberfest.com/), of which Winter is a supporter of. |
| hacktoberfest-accepted | No | Yes | The pull request is accepted as a valid Hacktoberfest entry. |
| help wanted | Yes | Yes | The maintainers have requested help with this issue or pull request. These are good candidates for new contributers to the project. |
| high priority | Yes | No | The maintainers have deemed that this issue needs to be more critically actioned. |
| low priority | Yes | No | The maintainers have deemed that this issue should be back-logged until things are less busy. We are still very much happy to accept pull requests should an external contributor wish to action this issue. |
| maintenance | No | Yes | Pull requests that fix bugs, update language files or make only minor changes. |
| needs docs | Yes | Yes | Issues or pull requests that require documentation changes in order to be completed. These can be actioned by the maintainers or external contributors. |
| needs pr | Yes | No | Issues that require a pull request to be completed. This is used by the maintainers when they accept a reported issue but need an external contributor to provide the pull request. |
| needs response | Yes | Yes | Issues or pull requests in which a maintainer is seeking more information regarding the submission. This is only used for questions asked in the comments - if a pull request needs changes to the code itself, this will be done through code review instead. |
| needs review | Yes | Yes | Issues or pull requests that require a review from a maintainer. |
| needs test case | Yes | Yes | Issues or pull requests in which a maintainer requires a test case to be submitted in order to further investigate or resolve the issue or pull request. |
| stale | Yes | Yes | Issues and pull requests that have had no recent activity and may be archived by the maintainers at any time. |
| third party | Yes | Yes | Issues and pull requests that are dependent on changes being made to a third-party library or system. |