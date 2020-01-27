The notes below reflect the changes and upgrade path for the October build that will contain the L6 upgrade.

## Testing instructions:

If you would like to help with the upgrade process please make the following changes in your composer.json file:

```json
"php": "^7.2",
"october/rain": "dev-wip/laravel-6 as 1.0",
"october/system": "dev-wip/laravel-6",
"october/backend": "dev-wip/laravel-6",
"october/cms": "dev-wip/laravel-6",
"laravel/framework": "~6.0",
```

## Breaking Changes:

- The minimum version of PHP supported is now PHP 7.2.9. Please note that the PHP 7.1 branch, and those before it, are now [unsupported](https://www.php.net/supported-versions.php).
- The version of Laravel has been changed from 5.5 LTS to 6.x LTS. If you are using packages made for Laravel you may have to go through and update them to a version compatible with Laravel 6.x.
- The Carbon library has been upgraded from version 1 to version 2. While this should mostly work with existing code, please [review the upgrade guide](https://carbon.nesbot.com/docs/#api-carbon-2).
- Cache TTL (time-to-live) values that are specified as an integer are treated as seconds now, as opposed to minutes, when interacting directly with a cache repository. If you interact with the cache directly, we recommend that you use `DateTime` or `Carbon` instances to define when your data is to expire (ex. `now()->addMinutes(60)` instead of `60`). If you wish to continue using integers, you will need to multiply your integer values by 60 to get the number of seconds. This does not affect the `cms.urlCacheTtl` and `cms.parsedPageCacheTTL` configuration values, which will continue to use minutes.

## Required changes

- Some new configuration files have been made available as part of the Laravel 6 upgrade. You must add these configuration files to your project's `config` folder, and adjust the configuration as necessary.
  - `config/auth.php` (link to auth.php on master)
  - `config/hashing.php` (link to hashing.php on master)
  - `config/logging.php` (link to logging.php on master)
- If your project uses Composer, the following changes must be made to your `composer.json` file in the project root folder:
  - Under the `require` section:
    - **php** must be changed to `^7.2`.
    - **laravel/framework** must be changed to `^6.0`.
  - Under the `require-dev` section:
    - **phpunit/phpunit** must be changed to `^8.0|^9.0`.
    - **meyfa/phpunit-assert-gd** must be changed to `^2.0`.
    - **dms/phpunit-arraysubset-asserts** must be added with `^2.0`.
  - Please see (link to composer.json on master) for an example on how `composer.json` should look.
- If you wish to use the October CMS unit tests, you must replace the `tests` folder in your project root folder with the updated `tests` folder from our Git repository. A .zip file of this folder can be found here: (link to tests.zip)
-

## Optional changes

- The following files have been updated for Laravel 6, however, you may continue to use your current version of these files if you wish.
  - `bootstrap/autoload.php`
  - `artisan`
-
