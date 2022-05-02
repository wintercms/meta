# Build 1.2.0 - Foundation framework upgrade (Laravel 9.x LTS)

Due to overwhelming support from the community, Winter CMS is updating its foundation framework to the latest Long Term Support (LTS) release. As a result, there are some new requirements to run Winter and some code changes required.

From the proposed Build 1.2.0 your webserver will require PHP 8.0.2 or above to use Winter CMS. After this date, websites using PHP 7.0-7.2.8 will still function normally but will no longer be able to receive updates or install the latest version.

There are various code changes that may be required, including code found in plugins and themes, both private and public depending on what features you are utilizing.

* Build 1.2.0 is available as a test update from 4 May 2021. Stable release date to be announced.

<a name="requirements"></a>
## New Minimum Requirements:

<a name="php-version"></a>
### Application Server
- PHP: 8.0.2

<a name="database-servers"></a>
### Database Servers
- MariaDB 10.2+ ([Version Policy](https://mariadb.org/about/#maintenance-policy))
- MySQL 5.7+ ([Version Policy](https://en.wikipedia.org/wiki/MySQL#Release_history))
- PostgreSQL 9.6+ ([Version Policy](https://www.postgresql.org/support/versioning/))
- SQLite 3.8.8+
- SQL Server 2017+ ([Version Policy](https://docs.microsoft.com/en-us/lifecycle/products/?products=sql-server))

<a name="dependencies"></a>
### Dependencies
- Laravel: 9.x
- Laravel Tinker: 2.7
- Twig: 3.x
- Symfony\Yaml: 5.1
- PHPUnit: 9.5.8
- Mockery: 1.4.4
- Assetic: 3.0

>**NOTE**: The PHP 7.4 branch, and those before it, are now [unsupported](https://www.php.net/supported-versions.php).

<a name="testing-instructions"></a>
## Testing instructions:
1. Change your composer.json requirements to the following and then run `composer update`:
```json
    "require": {
        "php": "^8.0.2",
        "winter/storm": "dev-wip/1.2 as 1.2",
        "winter/wn-system-module": "dev-wip/1.2",
        "winter/wn-backend-module": "dev-wip/1.2",
        "winter/wn-cms-module": "dev-wip/1.2",
        "laravel/framework": "^9.1",
        "wikimedia/composer-merge-plugin": "~2.0.1"
    },
    "require-dev": {
        "phpunit/phpunit": "^9.5.8",
        "mockery/mockery": "^1.4.4",
        "fakerphp/faker": "^1.9.2",
        "squizlabs/php_codesniffer": "^3.2",
        "php-parallel-lint/php-parallel-lint": "^1.0",
        "dms/phpunit-arraysubset-asserts": "^0.1.0|^0.2.1"
    },
```
2. If `config/app.php` makes reference to `Illuminate\Http\Request::HEADER_X_FORWARDED_ALL`, change it to `'HEADER_X_FORWARDED_ALL'`

<a name="upgrade-known-issues"></a>
## Known issues:

- **`Unexpected token "name" of value "if" ("end of statement block" expected).`:**
    - See https://twig.symfony.com/doc/2.x/deprecated.html#tags
    - Use the [`| filter` filter](https://twig.symfony.com/doc/3.x/filters/filter.html) or a conditional check inside of the loop block if the variable is affected by the contents of the loop.
    - This is most likely to affect users of the Winter.Pages plugin, simply update `{% for item in items if not item.viewBag.isHidden %}` to `{% for item in items | filter(item => not item.viewBag.isHidden) %}` in your custom partials.
- The str_contains() helper provided by Laravel has a slight signature mismatch compared to the one provided by the PHP 8.0 internals.

<a name="upgrade-required-changes"></a>
## Required code changes:

Any required code changes are described below in sections based on related functionality that you may or may not be using. If you are using the described functionality, please review the section and make the required changes.

Only potentially breaking changes are called out in this document, for the full list of all changes, please see the [1.2.0 release note](https://github.com/wintercms/meta/blob/master/release-notes/build-1.2.0.md).

<a name="upgrade-toc"></a>
## Affected functionality

If you are using any of the following functionality it's highly recommended that you take a look at the relevant section in this guide and make any required changes to your usage:

- [Twig](#upgrade-twig)
- [Configuration files (`/config/*.php`)](#upgrade-config)
- [Emails](#upgrade-emails)
- [Storage & Files](#upgrade-filesystems)
- [General Cleanup](#upgrade-cleanup)
- [Facades](#upgrade-facades)
- [Any packages made for Laravel](#upgrade-laravel-packages)
- [Unit Testing](#upgrade-unit-testing)

<a name="upgrade-twig"></a>
### Twig
- `$twigEnvironment->loadTemplate($name)` now requires `$cls` as the first parameter. Switch to `$twigEnvironment->load($name);` instead. See https://github.com/twigphp/Twig/commit/653dddd1f962e5cf6818f11e8757c82becd35a4f
- `{% filter %}` tag has been removed from Twig v3.0 (backported but use `{% apply %}` instead going forward)
- `{% spaceless %}` tag has been removed from Twig v3.0 (backported but use `{% apply spaceless %){% endapply %}` instead going forward)



<a name="upgrade-config"></a>
### Configuration Files
Review the changes to the [default configuration files](https://github.com/wintercms/winter/tree/wip/1.2/config) and implement any changes as desired; the following items are called out as potentially having an impact:

- `config/app.php`:
    - An application key is no longer provided by default, if your application does not yet have one set, run `artisan key:generate`.
    - `Illuminate\Http\Request::HTTP_X_FORWARDED_ALL` has been removed in Symfony 6, but it's referenced with no intermediate layer in the default app.php config file from v1.1.4 to v1.1.8. See https://github.com/wintercms/storm/commit/fcecefda3fd3966310306b5799852c53d6330a64 for more details.
- `config/database.php`:
    - Removed support for `database.useConfigForTesting`, use `config/testing/database.php` to override testing defaults instead.
    - Setting a `varcharmax` on `mysql` database connections is no longer supported as the minimum required version of MySQL now supports 255 character UTF8 strings by default.
- `config/mail.php`:
    - The structure has changed, update your local copy to match the one [now provided on the 1.2 branch](https://github.com/wintercms/winter/blob/wip/1.2/config/mail.php). The old one should continue working but it is recommended to update it to reflect the new structure.



<a name="upgrade-emails"></a>
### Emails
- Built in support for SES, Postmark, Mailgun, Mandrill, SendGrid, & SparkPost mail drivers has been removed, use the applicable first party driver plugins as needed:
    - [Winter.DriverAWS](https://github.com/wintercms/wn-aws-plugin)
    - [Winter.DriverMailgun](https://github.com/wintercms/wn-mailgun-plugin)
    - [Winter.DriverMandril](https://github.com/wintercms/wn-mandril-plugin)
    - [Winter.DriverPostmark](https://github.com/wintercms/wn-postmark-plugin)
    - [Winter.DriverSendGrid](https://github.com/wintercms/wn-sendgrid-plugin)
    - [Winter.DriverSparkPost](https://github.com/wintercms/wn-sparkpost-plugin)
- Review the [SymfonyMailer upgrade guide](https://laravel.com/docs/9.x/upgrade#symfony-mailer) if you interact with mail message objects directly, several methods and return types have changed.



<a name="upgrade-filesystems"></a>
### Storage & Files:
- The Rackspace Flysystem driver / adapter is no longer supported
- `Symfony\Component\HttpFoundation\File\UploadedFile->getClientSize()` has been removed, use `getSize()` instead.
- The `getAdapter()` method on Storage disks is no longer present. `getPathPrefix()` & `setPathPrefix()` methods have been added to the `$disk` instances if desired.



<a name="upgrade-cleanup"></a>
### Project Structure / General Cleanup:

- `server.php`:
    - It is no longer required for the `artisan serve` command to function if you haven't modified it from the default; it can be removed.



<a name="upgrade-facades"></a>
### Facades:
- Facades must return string keys rather than objects (See https://github.com/laravel/framework/pull/38017)
- `Winter\Storm\Support\Facades\Str` facade has been removed, use `Winter\Storm\Support\Str` directly instead.


<a name="upgrade-laravel-packages"></a>
### Using any Laravel based packages

The version of Laravel has been changed from 6.x LTS to 9.x LTS. If you are using packages made for Laravel you may have to go through and update them to a version compatible with Laravel 9.x.



<a name="upgrade-unit-testing"></a>
### Unit Testing

If you are running unit testing for Winter CMS development, you will need to make some changes to your composer.json file and replace the `tests` folder in your installation to get the updates to the unit tests.

**TODO: Complete this section after tests reorg is complete**



<a name="upgrade-guides"></a>
## Upgrade Guides:
- [PHP 8.0](https://www.php.net/manual/en/migration80.php)
- [PHP 8.1](https://www.php.net/manual/en/migration81.php)
- [Laravel 7](https://laravel.com/docs/7.x/upgrade)
- [Laravel 8](https://laravel.com/docs/8.x/upgrade)
- [Laravel 9](https://laravel.com/docs/9.x/upgrade)
- [SwiftMailer to Symfony Mailer](https://github.com/laravel/framework/pull/38481)
- [Symfony v5](https://github.com/symfony/symfony/blob/5.4/UPGRADE-5.0.md)
- [Symfony v6](https://github.com/symfony/symfony/blob/6.0/UPGRADE-6.0.md)
- [Twig 3.0](https://twig.symfony.com/doc/2.x/deprecated.html) ([changelog](https://github.com/twigphp/Twig/blob/3.x/CHANGELOG) & [announcement](https://symfony.com/blog/preparing-your-applications-for-twig-3))
- [Flysystem v2.0](https://flysystem.thephpleague.com/docs/upgrade-from-1.x/) & https://github.com/laravel/framework/pull/33612
- [Flysystem v3.0](https://flysystem.thephpleague.com/docs/what-is-new/) & https://github.com/laravel/framework/pull/40411
