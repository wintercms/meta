# Maintainers Guide to the Galaxy

## Introduction

This document immortalises the processes involved with maintaining the October CMS and RainLab
repositories. This is intended to give the maintainers of the project a clear idea as to how to 
review and manage the inflow of code and ensure the qualities and philosophies of October CMS and
the RainLab plugins are maintained.

## Roles

The project has two levels of maintainership. The current membership (as of December 11th, 2019)
is as follows:

**Lead Maintainers**

- [@alekseybobkov](https://github.com/alekseybobkov) - Aleksey Bobkov
- [@daftspunk](https://github.com/daftspunk) - Samuel Georges
- [@LukeTowers](https://github.com/LukeTowers) - Luke Towers

**Maintainers**

- [@w20k](https://github.com/w20k) - Denis Denisov
- [@bennothommo](https://github.com/bennothommo) - Ben Thomson
- [@mjauvin](https://github.com/mjauvin) - Marc Jauvin (RainLab Translate only)

Where possible, the access to all protocols below will be dictated by the roles above.

## Main Philosophy

October CMS operates under the philosophy that "Everything should be made as simple as possible,
but not simpler". As arbiters of the codebase, maintainers should strive to ensure that as the
functionality and potential of the system increases, careful thought is still given to ensuring
that proposed code is simple to develop for the developer and easy to use for the user.

Important reading on the philosophy of October CMS can be found through these links:

- https://octobercms.com/blog/post/getting-back-to-basics
- https://octobercms.com/blog/post/putting-octobercms-words
- https://octobercms.com/about

As October CMS is an "evergreen" product with rolling updates, special care must be taken to
maintain backwards compatibility and allow all users of October CMS and the RainLab plugins to
continue to use the products through updates without issue.

At the same time, October CMS has a responsibility to its users to ensure that best practices in
security and code are followed. Where possible, October CMS follows the LTS (long-term support)
versions of the Laravel framework as the foundation framework, which does include the deprecation
of unsupported PHP versions as required.

## Projects

### October CMS

The following protocols are in place for all current and future repositories underneath the
[@octobercms](https://github.com/octobercms) organisation. This includes the October CMS and Rain
library repositories, as well as its installer and documentation.

#### Main Branches

October CMS and the Rain library both have two main branches for their repositories - `master` 
and `develop`. Both branches represent the *stable* and *testing* states of the product - more 
specifically, they represent the most recent stable build and the most bleeding-edge publicly
available code, respectively.

In general, the only time `master` is updated is when a new stable version of October CMS is
released to the public. This process is done by the Lead Maintainers as part of their 
[Release Process](#release-process).

Direct commits to the `master` branch should not be done for the October CMS and Rain Library
repos except for the following circumstances:

- Pushing out a new stable release of October CMS *(Lead Maintainers only)*
- Making changes to any project-related meta or policy files, such as the README, funding,
licensing and security policies. *(Lead Maintainers only)*
- Fixing issues with the automated testing suite.
- Rectifying disclosed security vulnerabilities

For the installer and documentation repositories, commits to the `master` branch can be done on
an as-needed basis, as long as commits are small and are clearly explained and justified in the
commit message. It is still preferred that pull requests are used for larger commits. There is no
`develop` branch for these repositories.

#### Milestones

The October CMS and Rain libraries use milestones to track which changes are to be released with
each build. Although October CMS is a continously-developed evergreen project, milestones are
named in a version format like so in order to reflect the final "tag" that is made when a new
build is released:

- `v1.0.459`
- `v1.0.460`
- `v1.0.461`

In these examples, the final number represents the build number, with `v1.0.` prefixed to the
build number to match versioning standards.

One build milestone representing the *next* build to be released will be present for all
incoming code changes. In some cases, a second build milestone representing the version after
this will also be available should the first build milestone be locked from further changes.
For example, if the last build released was build 459, there will be a milestone for 460, and
potentially 461 as well.

Two special milestones have also been created as "staging" areas for incoming changes:

- **In Progress:** Issues and Pull Requests assigned to this milestone represent changes that have
been accepted by the maintainers for inclusion in the codebase, but are not yet finished by the
submitter.
- **Pending Features:** Issues and Pull Requests assigned to this milestone represent finished
features and fixes that are ready to be included in an upcoming build. A maintainer may "sponsor"
a feature to be included in a build, which represents their intention to test and approve the
feature or fix, and maintain it once it has been merged into the codebase.

#### Reviewing Issues and Pull Requests

Maintainers must review all issues and pull requests that are made to the October CMS repositories
to ensure that they meet the standards of code quality and adherence to the principles of October
CMS.

Things that maintainers should look at with issues should include:

- If it is a reported bug, does the bug exist? Sometimes bugs are due to configuration issues,
or unique environments.
- If it is a suggested enhancement or change, does it solve a problem that October does not yet
solve?
- If it is a discussion, again, is the discussion towards finding a solution to a problem that
October does not yet cover?

When reviewing pull requests, maintainers should strive to look at the following:

- Does the pull request actually solve the issue it intends to resolve?
- Does the pull request follow the [PSR-2 guidelines](https://www.php-fig.org/psr/psr-2/) and 
our own [Developer Guidelines](https://octobercms.com/help/guidelines/developer)?
- Does the pull request allow users of October CMS to continue to use the system as they have
up until now, or provide adequate justification for the change in behaviour?

Pull requests submitted by contributors must be made to the `develop` branch or to a feature or
fix branch - any pull requests made to the `master` branch must be rebased to `develop`. In these
cases, it is generally best to indicate to the contributor that the `master` branch is not the
correct base (you can use this
[standard reply](https://github.com/octoberrain/meta/blob/master/github/saved-replies/wrong-branch.md)
for this).

Pull requests should also indicate any issues that they resolve - this should be stipulated as
"Fixes #..." followed by the issue number in the first comment of a pull request thread.

Maintainers have free reign to ask for clarification on issues and PRs and seek further information
from the submitter. If more details are not forthcoming, maintainers may close the issue or PR. In
addition, issues and PRs are automatically closed after 30 days of inactivity.

To keep track of the progress of issues and pull requests, we use the labelling and milestone
systems of GitHub to record the current status. Our
[standard labels](https://github.com/octoberrain/meta/blob/master/github/labelling.md) dictate a 
type of pull request or issue (ie. an enhancement, maintenance, discussions or bug report), a status
(ie. in progress, completed, or a response or revision is needed) and sometimes a priority (ie. 
critical, high or low). In general, an issue should have one type label and one status label.

If an issue or pull request is accepted, it should be assigned to either the **In Progress**
milestone if it is not yet completed, or the **Pending Features** milestone if it is completed but
is not yet determined which build it will be implemented in. Once a build has been decided, the
milestone should be set to the build milestone.

#### Merging Pull Requests

When a Pull Request is assigned to the *current* build milestone, it can be merged into the `develop`
branch. Maintainers should use the **Squash and merge** option in GitHub to squash PRs into one
commit that is then merged into the `develop` branch. This function creates a commit with the name
of the PR followed by the PR number in parenthesis to give a quick and useful link back to the merged
PR.

The commit message should contain extra information about the merged PR if it is applicable - this
should include any justifications for the change and important info that might be required for
future reference.

As a show of appreciation for contributor submissions, we make sure that the committer is credited
for the commit in the commit message - credit is given as a `Credit to @user` message provided at
the bottom of the commit message. In addition, any fixed or referenced issues or PRs should be linked
as well, tagged as either `Fixed:` or `Refs:` respectively. GitHub will automatically link any issue
numbers added to the same repository, but external repositories should be linked as a URL.

An example commit message is below:

```
Fix some issues in the code (#1234)

This fixes a couple of issues spotted in the Backend. The changes are minor and should not affect backwards compatibility.

Credit to @bennothommo. Fixes #1212 and https://github.com/rainlab/blog#432
```

A merged pull request - and any linked issues that the pull request resolves - should have the
`Status: Completed` label assigned to them and all other Status labels should be unassigned. If the
pull request does not have a build milestone assigned to it yet, this should also be changed to the
current build milestone.

#### Standard Workflow for Maintainers

Where possible, all work done on October CMS should be done through pull requests. Pull requests
allow the opportunity for all maintainers to be able to review the proposed changes and provide
feedback or determine any perceived issues, and in addition allow the automated tests to pick up
any issues with code quality or our test scenarios before it reaches the main branches.

Maintainers should create a branch for their incoming changes - using the following format for
the branch name:

- `wip/` followed by the feature name in kebab-case for a new feature.
- `fix/` followed by either a fix name in kebab-case, or alternatively, an issue number if the fix
is to resolve a reported issue on GitHub.

Pull requests must be made to the `develop` branch and provide a succint description as the title
of the pull request, with more information as required for other maintainers to understand the
changes implemented.

Direct commits to the `develop` branch should be avoided where possible in favour of pull requests. A
few circumstances exist where a commit straight to `develop` may be necessary:

- Fixing parse errors or exceptions that may have been missed during code review of a PR.
- Documentation fixes.
- Fixing disclosed security vulnerabilities.
- Minor tweaks that do not change any current behaviours of October CMS.
