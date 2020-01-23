The notes below reflect the changes and upgrade path for the October build that will contain the L6 upgrade.

## Breaking changes

- The Laravel 6 upgrade requires PHP to be at least version 7.2.9 or above. If you cannot upgrade to this version, you will
need to remain on build (build number before upgrade). Please note that the PHP 7.1 branch, and those before it, are now
[unsupported](https://www.php.net/supported-versions.php).
- The Carbon library, which provides date and time manipulation in October CMS, has been upgraded from version 1 to 2. This may
be incompatible with some October CMS plugins and Laravel plugins in use. You will need to upgrade your plugins to a version
that uses Carbon v2, if available. If no version is available, you will need to remain on build (build number before upgrade)
or cease using that particular plugin.
- Cache TTL (time-to-live) values that are specified as an integer are treated as seconds now, as opposed to minutes, when
operating directly with a cache repository. If you interact with the cache directly, we recommend that you use `DateTime` or `Carbon` instances to define when your data is to expire. If you wish to continue using integers, you will need to multiply
your integer values by 60 to get the number of seconds. This does not affect the `cms.urlCacheTtl` and `cms.parsedPageCacheTTL` configuration values, which will continue to use minutes.
-

## Required changes

- Some new configuration files have been made available as part of the Laravel 6 upgrade. You must add these configuration
files to your project's `config` folder, and adjust the configuration as necessary.
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
- If you wish to use the October CMS unit tests, you must replace the `tests` folder in your project root folder with the
updated `tests` folder from our Git repository. A .zip file of this folder can be found here: (link to tests.zip)
-

## Optional changes

- The following files have been updated for Laravel 6, however, you may continue to use your current version of these files
if you wish.
  - `bootstrap/autoload.php`
  - `artisan`
-
