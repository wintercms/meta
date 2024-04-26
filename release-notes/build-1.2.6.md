# Build 1.2.6

## UX/UI Improvements
- Improved UX when invalid dates are present in a datepicker field by displaying a warning message and allowing the user to edit those values. Also improved support for date values that use `.` as a separator.

## API Changes
- The `Illuminate\Http\Middleware\HandleCors` middleware is now included in the core HTTP kernel by default. In order to start using the CORS support added by this change add the `config/cors.php` file to your project and configure it accordingly.
- Added `--no-progress` and `--json` options to `mix:compile`, `mix:watch`, & `mix:list` commands.
- Added support for the List widget's `showPageNumbers` in `RelationController`'s `view` and `manage` configuration scopes.
- Added support for logging context data in the backend `EventLog`.
- Added support for the `array_*()` helper functions in the System Twig environment.
- The `date()` Twig filter and function now run through the `System\Helpers\DateTime` helper to process them with Carbon.

## Bug Fixes
- Fixed an issue where `HasOneThrough` and `HasManyThrough` relationships were not taking the `count` and `scope` relationship configuration options into account.
- Fixed an issue where `ignore_missing` wasn't being respected in the `source()` Twig function.

## Dependencies
- Twig has been locked to 3.8 as 3.9 introduces a breaking change. 3.9+ will be supported in the next release.
- FontAwesome has been updated to 6.5.2 and the asset compilation step has been moved to Winter Mix for easier upgrades in the future. This also removes the vendor files for FontAwesome from the repository.
- The customized styles for Select2 in the Winter backend are now compiled to a standalone file (`/modules/system/assets/ui/vendor/select2/css/select2.css`).
