# Build 1.2.16 (WIP)

## API Changes
- This release adds a nullable `backend_users.reset_password_created_at` column, so run `php artisan winter:up` as part of deploying it. Between the code landing and the migration running, both the public restore form and the administrator reset button error.
- Backend password reset codes now expire and are limited in how often they can be re-issued, read from Laravel's own `auth.passwords.backend.expire` (minutes, default 60) and `auth.passwords.backend.throttle` (seconds, default 60). While the re-issue window is open the restore form issues nothing and mails nothing, which leaves the code already in the account holder's inbox valid rather than replacing it. A throttle of `0` restores unlimited re-issue, matching Laravel.
- The administrator-triggered password reset now verifies the request host, as the public restore form has since v1.1.2. On an install with trusted hosts disabled whose `app.url` does not name the host the backend is served on, that button now fails rather than mailing a link to the wrong domain.
- `create`, `update` and `preview` no longer route on `System\Controllers\MailBrandSettings`, and `create` and `update` no longer route on `Cms\Controllers\ThemeLogs`, `System\Controllers\EventLogs` and `System\Controllers\RequestLogs`. `index` and `preview` are unchanged, as are the handlers those actions serve. A controller subclassing one of these to add a form screen must declare its own `$guarded`.
- A controller subclassing `Cms\Controllers\ThemeOptions` and overriding `formExtendQuery()` must call `parent::formExtendQuery($query)` to keep the active-theme restriction.
- An export file now belongs to the backend user who generated it. `ExportModel::export()` and `ThemeExport::export()` require an authenticated user, where before they would write a file nobody could be served, and a plugin that writes its own file into `temp_path()` and hands the name to `ExportModel::download()` must write it through `getExportFilePath()`. `Backend\Traits\ExportFileStorage` carries `makeExportFileName()`, `getExportFilePath()` and `findExportFilePath()`.

## Security Improvements
- Hardened the backend password reset flow.
- Hardened the authorization of inherited backend form and export handlers, and of the files the export flows leave behind.
