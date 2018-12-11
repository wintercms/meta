The OctoberCMS, OctoberRain, & RainLab GitHub organizations use the following system of labels for managing issues and pull requests. Every issue  / pull request should generally at least have a Type label and Status label assigned to them. Priority & Miscellaneous labels can be assigned as applicable.

## Types
| Label                        | Description / Purpose                                                |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Type: Unconfirmed Bug        | Bug that has been reported but not yet verified / reproduced by a maintainer or trusted community member yet                   |
| Type: Bug                    | Bug that has been identified / verified as an issue that needs to be resolved as it relates to incorrect behavior of code      |
| Type: Conceptual Enhancement | A proposed enhancement that has not been implemented yet but is still in the discussion stage                                  |
| Type: Enhancement            | A proposed enhancement that has been implemented                                                                               |
| Type: Maintenance            | Issue / PR that consists of minor maintenance to the code base (i.e. minor bug fixes, styling fixes, translation improvements) |
| Type: Discussion             | Issue that is meant for discussion between members of the community                                                            |
| Type: Question               | Issue that is actually just a question                                                                                         |


## Statuses
| Label                        | Description / Purpose                                                |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Status: Abandoned            | Issue / PR that has not seen any activity in at least a month, used to prompt stakeholders to take interest in the issue again |
| Status: Accepted             | Issue / PR (usually a feature request or conceptual enhancement) that has been approved in theory.                             |
| Status: Blocked              | Issue / PR that is blocked from progressing by something (usually another related issue / PR)                                  |
| Status: Completed            | Issue / PR that has been completed and merged into the `develop` branch and is remaining open until it has been merged into master |
| Status: In Progress          | Issue / PR that is currently being worked on                                                                                   |
| Status: On Hold              | Issue / PR that has been put on hold for now but will be worked on again in the future                                         |
| Status: Pending              | Issue / PR that is waiting for something else to happen before it will be worked on                                            |
| Status: Response Needed      | Issue / PR that requires / is waiting on a response from at least one of the participants                                      |
| Status: Review Needed        | Issue / PR that requires review from a maintainer or trusted community member                                                  |
| Status: Revision Needed      | Issue / PR that requires changes before it can be accepted                                                                     |


## Priorities
| Label                        | Description / Purpose                                                |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Priority: Critical           | Critical issue that needs to get addressed immediately, i.e. breaking build or composer release or security vulnerability      |
| Priority: High               | Issue that should be resolved for inclusion in the next build                                                                  |
| Priority: Medium             | Issue that is on the horizon to be addressed at some point                                                                     |
| Priority: Low                | Issue / PR that in theory would be accepted, but maintainers aren't planning on working on it any time soon.                   |


## Miscellaneous Labels

| Label                        | Description / Purpose                                                |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| duplicate                    | Issue / PR is a duplicate of another and is being closed in favour of the other                                                |
| good first issue             | Issue / PR is a good candidate for newcomers to the project to begin contributing on                                           |
| hacktoberfest                | Issue / PR would be a good fit for Hacktoberfest contributions                                                                 |
| help wanted                  | Makes the issue / PR show up in GitHub's list of Help Wanted issues / PRs                                                      |
| PostgreSQL                   | Issue / PR is related to PostgreSQL compatibility                                                                              |
| third party                  | Issue / PR is not related to the repository, it must be handled by a third party instead                                       |
| wrong branch                 | Should not be used anymore as maintainers can edit the branch a PR is made to themselves                                       |
| Website / Marketplace / Docs | Issue is related to the OctoberCMS.com marketplace or documentation                                                            |