# Build 1.1.5 (WIP)

## UX/UI Improvements
- Added a notice to the top of every page in the backend when using the user impersonation functionality. <img width="1246" alt="Screen Shot 2021-08-24 at 2 03 38 PM" src="https://user-images.githubusercontent.com/7253840/130687384-306d0a07-da46-42d6-a6fc-b6810ae4c6c0.png">


## API Changes
- Added `getRealUser()` to `Winter\Storm\Auth\Manager` to get the real user for the current request, taking into account user impersonation
- Added `canBeImpersonated($impersonator = false)` to `Winter\Storm\Auth\Models\User` and models extending it (i.e. `Backend\Models\User`); used to determine if the provided impersonator can impersonate the selected user.
- Changed `model.user.beforeImpersonate` to a halting event so that third party plugins are able to override the default return values from canBeImpersonated() to implement more or less strict impersonation protection policies as desired on a per project basis by returning a boolean flag indicating if the user can be impersonated or not

## Bug Fixes
- Fixed critical issue introduced in 1.1.4 where `post()` didn't return the default value when the request was not a POST request. This caused issues with forms relying on session keys (i.e. file upload fields etc.) as well as the form context property.

## Security Improvements
- Triggering user impersonation while already impersonating a user will now record the original impersonator as the impersonator for the second impersonation action as well, previously the impersonated user would have been recorded as the impersonator in those cases.
- Impersonated users will now have their access filtered to only include permissions that the impersonator would have also had access to.
- CMS Theme logs now reflect the real user behind a request; taking into account user impersonation.

## Translation Improvements
-

## Performance Improvements
-

## Community Improvements
-

## Dependencies
-
