# Build 4XX - Foundation framework upgrade (Laravel 6.x LTS)

Release Note 10

Due to overwhelming support from the community, October CMS is updating its foundation framework to the latest Long Term Support (LTS) release. As a result, there are some new requirements to run October and some code changes required.

From the proposed date of 1st March 2020* (Build 4XX) your webserver will require PHP 7.2.9 or above to use October CMS. After this date, websites using PHP 7.0-7.2.8 will still function normally but will no longer be able to receive updates or install the latest version.

There are various code changes that may be required, including code found in plugins and themes, both private and public depending on what features you are utilizing.

Instructions marked with a `√` can be performed immediately to ensure forward compatibility. In other words the change is compatible with all versions of October, now and after the release. It is recommended to make these changes as soon as possible.

* Build 4XX is available as a test update from 15th Febraury 2020. Stable release date to be announced.

## New system requirements:

- PHP 7.2.9 or greater (recommended PHP 7.4)
- SQLite 3.7.11 or greater (recommended SQLite 3.8.8+)

>**NOTE**: The PHP 7.1 branch, and those before it, are now [unsupported](https://www.php.net/supported-versions.php).

## Known issues:

-

## Testing instructions:

If you would like to help with the upgrade process please make the following changes in your composer.json file and then run `composer update`.

```json
"require": {
    "php": "^7.2",
    "ext-mbstring": "*",
    "ext-openssl": "*",
    "october/rain": "dev-wip/laravel-6 as 1.0",
    "october/system": "dev-wip/laravel-6",
    "october/backend": "dev-wip/laravel-6",
    "october/cms": "dev-wip/laravel-6",
    "laravel/framework": "~6.0",
    "wikimedia/composer-merge-plugin": "dev-master"
},
"config": {
    "preferred-install": "dist"
},
```

## Required code changes:

Any required code changes are described below in sections based on related functionality that you may or may not be using. If you are using the described functionality, please review the section and make the required changes.

### Git repositories

If you track your project in a Git repository, you will need to add the `storage/framework/cache/data/.gitignore` file to your project with the following contents:

```
*
!.gitignore
```

as well as add `!data/` to the `storage/framework/cache/.gitignore` file.

### Composer (composer.json)

If you are using composer you will need to make the following changes to your composer.json file:

```json
"require": {
    "php": "^7.2",
    "ext-mbstring": "*",
    "ext-openssl": "*",
    "october/rain": "dev-wip/laravel-6 as 1.0",
    "october/system": "dev-wip/laravel-6",
    "october/backend": "dev-wip/laravel-6",
    "october/cms": "dev-wip/laravel-6",
    "laravel/framework": "~6.0",
    "wikimedia/composer-merge-plugin": "dev-master"
},
"config": {
    "preferred-install": "dist"
},
```

### Configuration files (`config/*` files)

Some new configuration files have been made available as part of the Laravel 6 upgrade. You should add these configuration files to your project's `config` folder, and adjust the configuration as necessary. While you're doing that, it is recommended that you review the rest of the configuration files present on GitHub and ensure that your project's copies are up to date as there have been numerous configuration options added over the past year.

  - [`config/hashing.php`](https://github.com/octobercms/october/blob/wip/laravel-6/config/hashing.php)
  - [`config/logging.php`](https://github.com/octobercms/october/blob/wip/laravel-6/config/logging.php)

### Environment variables (`.env` files)

If you are using `.env` files with a variable that has a `#` inside of an unquoted value; that will now be treated as a comment due to an upgrade to the `phpdotenv` library used for parsing them.

If you have any `#` characters inside of unquoted environment variables please update them to be quoted instead (ex. `DB_PASS=23das#sdfas` must be updated to `DB_PASS="23das#sdfas"`).

Additionally, `putenv()` no longer changes the value returned by calls to `env()` as the `env` helper is now considered read-only. If dynamically changing configuration is required, it is recommended to use Config values instead as they can be dynamically changed with `Config::set()`

### Using any Laravel based packages

The version of Laravel has been changed from 5.5 LTS to 6.x LTS. If you are using packages made for Laravel you may have to go through and update them to a version compatible with Laravel 6.x.

### Interacting with Cache repositories directly

Cache TTL (time-to-live) values that are specified as an integer are treated as seconds now, as opposed to minutes, when interacting directly with a cache repository. If you interact with the cache directly, we recommend that you use `DateTime` or `Carbon` instances to define when your data is to expire (ex. `now()->addMinutes(60)` instead of `60`). If you wish to continue using integers, you will need to multiply your integer values by 60 to get the number of seconds.

>**NOTE**: This does not affect the `cms.urlCacheTtl` and `cms.parsedPageCacheTTL` configuration values, which will continue to use minutes.

### String-based primary keys in models

If you are using string based primary keys for your models add `protected $keyType = 'string';` to the model class definition to prevent performance optimizations meant for integer key types from negatively affecting your code.

### Using Carbon directly

The Carbon library has been upgraded from version 1 to version 2. While this should mostly work with existing code, please [review the upgrade guide](https://carbon.nesbot.com/docs/#api-carbon-2).

### Using Symfony directly

Symfony has been upgraded to version 4. If interacting directly with it, please [review the upgrade guide](https://github.com/symfony/symfony/blob/master/UPGRADE-4.0.md)

### Optional changes

The following files have been updated for Laravel 6, however, you may continue to use your current version of these files if you wish:

  - [`bootstrap/autoload.php`](https://github.com/octobercms/october/blob/wip/laravel-6/bootstrap/autoload.php)
  - [`artisan`](https://github.com/octobercms/october/blob/wip/laravel-6/artisan)

### Unit Testing

If you are using unit testing, you will need to make some changes to your composer.json file, the `tests/` directory, and your unit tests themselves.

**composer.json** changes required:
```json
"require-dev": {
    "fzaninotto/faker": "^1.9",
    "phpunit/phpunit": "^8.0|^9.0",
    "phpunit/phpunit-selenium": "dev-master",
    "dms/phpunit-arraysubset-asserts": "^0.1.0",
    "meyfa/phpunit-assert-gd": "^2.0",
    "squizlabs/php_codesniffer": "3.*",
    "jakub-onderka/php-parallel-lint": "^1.0"
},
"autoload-dev": {
    "classmap": [
        "tests/concerns/InteractsWithAuthentication.php",
        "tests/fixtures/backend/models/UserFixture.php",
        "tests/TestCase.php",
        "tests/UiTestCase.php",
        "tests/PluginTestCase.php"
    ]
},
"scripts": {
    "post-create-project-cmd": [
        "php artisan key:generate",
        "php artisan package:discover"
    ],
    "post-update-cmd": [
        "php artisan october:util set build",
        "php artisan package:discover"
    ],
    "test": [
        "phpunit --stop-on-failure --prepend ./vendor/october/rain/src/Support/helpers.php"
    ],
    "lint": [
        "parallel-lint --exclude vendor --exclude storage --exclude tests/fixtures/plugins/testvendor/goto/Plugin.php ."
    ],
    "sniff": [
        "phpcs --colors -nq --report=\"full\" --extensions=\"php\""
    ]
},
```

You then need to replace the contents of your project's `tests/` directory with the [`tests/` directory from the repository](https://github.com/octobercms/october/tree/wip/laravel-6/tests). Additionally, you will need to update any of your unit tests that have `setUp()` or `tearDown()` methods to also include a `: void` return type hint as the version of PHPUnit used now includes those type hints in the base classes.

## Further reading

### Laravel Upgrade Guides:

- [5.5 -> 5.6](https://laravel.com/docs/5.6/upgrade)
- [5.6 -> 5.7](https://laravel.com/docs/5.7/upgrade)
- [5.7 -> 5.8](https://laravel.com/docs/5.8/upgrade)
- [5.8 -> 6.x](https://laravel.com/docs/6.x/upgrade)

### Package Upgrade Guides

- [Carbon](https://carbon.nesbot.com/docs/#api-carbon-2)
- [Symfony](https://github.com/symfony/symfony/blob/master/UPGRADE-4.0.md)
- [phpdotenv](https://github.com/vlucas/phpdotenv/blob/master/UPGRADING.md#v2-to-v3)

### PHP Upgrade Guides

**Migrating from PHP 7.0 to PHP 7.1**
- [Deprecated features in PHP 7.1](https://www.php.net/manual/en/migration71.deprecated.php)
- [Backwards-incompatible changes](https://www.php.net/manual/en/migration71.incompatible.php)

**Migrating from PHP 7.1 to PHP 7.2**
- [Deprecated features in PHP 7.2](https://www.php.net/manual/en/migration72.deprecated.php)
- [Backwards-incompatible changes](https://www.php.net/manual/en/migration72.incompatible.php)

**Migrating from PHP 7.2 to PHP 7.3**
- [Deprecated features in PHP 7.3](https://www.php.net/manual/en/migration73.deprecated.php)
- [Backwards-incompatible changes](https://www.php.net/manual/en/migration73.incompatible.php)

**Migrating from PHP 7.3 to PHP 7.4**
- [Deprecated features in PHP 7.4](https://www.php.net/manual/en/migration74.deprecated.php)
- [Backwards-incompatible changes](https://www.php.net/manual/en/migration74.incompatible.php)