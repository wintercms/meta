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
1. Change the following composer.json requirements:
```json
    "require": {
        "php": "^8.0.2",
        "winter/storm": "~1.2.0",
        "winter/wn-system-module": "~1.2.0",
        "winter/wn-backend-module": "~1.2.0",
        "winter/wn-cms-module": "~1.2.0",
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
2. If you have the following lines in your `composer.json` file, please remove these:
```json
    "autoload-dev": {
        "classmap": [
            "tests/concerns/InteractsWithAuthentication.php",
            "tests/fixtures/backend/models/UserFixture.php",
            "tests/TestCase.php",
            "tests/PluginTestCase.php"
        ]
    },
```
3. You may also delete the `tests` folder completely, as these testing files now reside in the modules, unless you have your own tests within this folder.
3. Run `composer update`.
4. If `config/app.php` makes reference to `Illuminate\Http\Request::HEADER_X_FORWARDED_ALL`, change it to `'HEADER_X_FORWARDED_ALL'`

<a name="upgrade-known-issues"></a>
## Known issues:

- **`Unexpected token "name" of value "if" ("end of statement block" expected).`:**
    - See https://twig.symfony.com/doc/2.x/deprecated.html#tags
    - Use the [`| filter` filter](https://twig.symfony.com/doc/3.x/filters/filter.html) or a conditional check inside of the loop block if the variable is affected by the contents of the loop.
    - This is most likely to affect users of the Winter.Pages plugin, simply update `{% for item in items if not item.viewBag.isHidden %}` to `{% for item in items | filter(item => not item.viewBag.isHidden) %}` in your custom partials.
- The `str_contains()` helper provided by Laravel has a slight signature mismatch compared to the one provided by the PHP 8.0 internals.

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
- [Storm Library Internals](#upgrade-storm-internals)
- [Upgrade Guides](#upgrade-guides)

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
    - The structure has changed, update your local copy to match the one [now provided on the develop branch](https://github.com/wintercms/winter/blob/develop/config/mail.php). The old one should continue working but it is recommended to update it to reflect the new structure.
- `config/filesystems.php`:
    - The `local` disk currently needs a `visibility => 'public'` setting in order for the files/folders under `/storage/app/resized` to be publicly accessible when using the image resizer.


<a name="upgrade-emails"></a>
### Emails
- Built in support for SES, Postmark, Mailgun, Mandrill, SendGrid, & SparkPost mail drivers has been removed, use the applicable first party driver plugins as needed:
    - [Winter.DriverAWS](https://github.com/wintercms/wn-driveraws-plugin)
    - [Winter.DriverMailgun](https://github.com/wintercms/wn-drivermailgun-plugin)
    - [Winter.DriverMandrill](https://github.com/wintercms/wn-drivermandrill-plugin)
    - [Winter.DriverPostmark](https://github.com/wintercms/wn-driverpostmark-plugin)
    - [Winter.DriverSendGrid](https://github.com/wintercms/wn-driversendgrid-plugin)
    - [Winter.DriverSparkPost](https://github.com/wintercms/wn-driversparkpost-plugin)
- Review the [SymfonyMailer upgrade guide](https://laravel.com/docs/9.x/upgrade#symfony-mailer) if you interact with mail message objects directly, several methods and return types have changed.



<a name="upgrade-filesystems"></a>
### Storage & Files:
- The Rackspace Flysystem driver / adapter is no longer supported
- `Symfony\Component\HttpFoundation\File\UploadedFile->getClientSize()` has been removed, use `getSize()` instead.
- The `getAdapter()` method on Storage disks is no longer present. `getPathPrefix()` & `setPathPrefix()` methods have been added to the `$disk` instances if desired.



<a name="upgrade-localization"></a>
### Localization:

The `translator.beforeResolve` event has been removed for performance reasons. `Lang::set($key, $value, $locale)` can be used as a replacement.

#### Overriding a specific key:

**Winter < v1.2**
```php
 Event::listen('translator.beforeResolve', function ($key, $replaces, $locale) {
    if ($key === 'validation.reserved') {
        return Lang::get('winter.builder::lang.validation.reserved');
    }
});
```
**Winter >= v1.2**
```php
Lang::set('validation.reserved', Lang::get('winter.builder::lang.validation.reserved'));
```

#### Overriding an entire namespace:

If you were using the event to extend / override an entire namespaced key (for example in order to share localization overrides that would normally be present in a project's `lang` override folder at the project root between multiple projects via a plugin), then you could switch your code to use the following example:

```php
Lang::set('winter.builder::lang', require __DIR__ . '/lang/en-ca/lang.php', 'en-ca');
```



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

If you are running unit testing for Winter CMS development, you will need to make some changes to your composer.json file and remove the `tests` folder from your installation to get the updates to the unit tests.

This block of code is no longer required in your `composer.json` file:

```json
    "autoload-dev": {
        "classmap": [
            "tests/concerns/InteractsWithAuthentication.php",
            "tests/fixtures/backend/models/UserFixture.php",
            "tests/TestCase.php",
            "tests/PluginTestCase.php"
        ]
    },
```

Since the testing files now reside within the modules folder, you may need to update your `phpunit.xml` configuration files and test cases if they make reference to any files in their old locations. To help ease the transition, you may use the `php artisan winter:test -p <your plugin code>` command, which will use the correct bootstrap file for Winter 1.2 testing. You may keep the old `bootstrap` configuration in your `phpunit.xml` file if you wish to test both Winter 1.1 and 1.2.

Since the base `PluginTestCase` class has also been moved, any test case files that are extending this class will need to either update the reference to `\System\Tests\Bootstrap\PluginTestCase`, or alternatively, you can use the following code to support testing on both Winter 1.1 and 1.2:

```php
// Create a stub BaseTestCase that extends the correct plugin test case file depending on Winter version
if (class_exists('System\Tests\Bootstrap\PluginTestCase')) {
    class BaseTestCase extends \System\Tests\Bootstrap\PluginTestCase
    {
    }
} else {
    class BaseTestCase extends \PluginTestCase
    {
    }
}

class MyTestCase extends BaseTestCase
```

<a name="upgrade-storm-internals"></a>
### Storm Library Internals

Version 1.2 of Winter includes a large code refactoring and documentation cleanup for the Storm library, to ensure that our base functionality is fully documented and works in a consistent and expected way. In addition, this brings our Storm library closer to the base Laravel functionality, which should make upgrades quicker and less painful in the future.

While we have ensured that the potential for breaking changes is low, there may be some cases of breaking functionality if the functionality used an undocumented or incorrectly-documented API. We will list all the changes below, grouped by the "package" within the Storm library:

- [\Winter\Storm\Database](#storm-database)
- [\Winter\Storm\Extension](#storm-extension)
- [\Winter\Storm\Filesystem](#storm-filesystem)
- [\Winter\Storm\Foundation](#storm-foundation)
- [\Winter\Storm\Halcyon](#storm-halcyon)
- [\Winter\Storm\Html](#storm-html)
- [\Winter\Storm\Parse](#storm-parse)
- [\Winter\Storm\Support\Testing](#storm-support-testing)

<a name="storm-database"></a>
#### Database

- To prevent unsafe model instantiating, the model constructors are now forced to only allow a single `$attributes` parameter via an interface (`\Winter\Storm\Database\ModelInterface` and `\Winter\Storm\Halcyon\ModelInterface`). This will ensure that calls like `Model::make()` or `Model::create()` will execute correctly. It is possible that some people might have used additional parameters for their model constructors - these will no longer work and must be moved to another method.
- Due to the above, Pivot model construction has been rewritten. The constructor used to allow 4 parameters but now only allows the one `$attributes` parameter as per the Model class. Construction now happens more closely to Laravel's format of calling a `Pivot::fromAttributes()` static method. If you previously used `new Pivot()` to create a pivot model, switch to using `Pivot::fromAttributes()` instead.
- The `MorphToMany` class now extends the `MorphToMany` class from Laravel, as opposed to the `BelongsToMany` class in Winter. This prevents repeated code in the Winter `MorphToMany` class and maintains covariance with Laravel. This will mean that it will no longer inherit from the Winter `BelongsToMany` class. To allow for this, we have converted most of the overridden `BelongsToMany` functionality in Winter into a trait (`Concerns\BelongsOrMorphsToMany`). The `BelongsToMany` relation class now also uses this trait.
- The relation traits found in `src/Database/Relations` have been moved to `src/Database/Relations/Concerns`, in order to keep just the actual relation classes within the `src/Database/Relations` directory. In the unlikely event that you are using a relation trait directly, please rename the trait classes to the following:
    - `Winter\Storm\Database\Relations\AttachOneOrMany` to `Winter\Storm\Database\Relations\Concerns\AttachOneOrMany`
    - `Winter\Storm\Database\Relations\DeferOneOrMany` to `Winter\Storm\Database\Relations\Concerns\DeferOneOrMany`
    - `Winter\Storm\Database\Relations\DefinedConstraints` to `Winter\Storm\Database\Relations\Concerns\DefinedConstraints`
    - `Winter\Storm\Database\Relations\HasOneOrMany` to `Winter\Storm\Database\Relations\Concerns\HasOneOrMany`
    - `Winter\Storm\Database\Relations\MorphOneOrMany` to `Winter\Storm\Database\Relations\Concerns\MorphOneOrMany`

<a name="storm-extension"></a>
#### Extension

- Previously, the `Winter\Storm\Extension\Extendable::extendClassWith()` method returned the current class if the extension name provided was an empty string. This appears to be a code smell, so this has been changed to throw an Exception.

<a name="storm-filesystem"></a>
#### Filesystem

- The `Filesystem::symbolizePath` method's `$default` parameter now accepts a `string`, `bool` or `null`. Only in the case of `null` will the method return the original path - the given `$default` will be used in all other cases. This is the same as the original functionality, but we're documenting it in case you have customised this method in some fashion.
- The `Filesystem::isPathSymbol` method previously returned the path symbol used, as a string, if one was found and `false` if not found. However, the docblock stipulated, as well as the method name itself implied, that this is a boolean check function, so we have converted this to a straight boolean response - `true` if a path symbol is used, otherwise `false`.
- Many classes within the `Filesystem` namespace have had type hinting and return types added to enforce functionality and clarify documentation. If you extend any of these classes in your plugins, you may need to update your method signatures.

<a name="storm-foundation"></a>
#### Foundation

- The `Winter\Storm\Foundation\Application` class callback methods `before` and `after` were documented as `void` methods, but returned a value. These no longer return a value.

<a name="storm-halcyon"></a>
#### Halcyon

- To prevent unsafe model instantiating, the model constructors are now forced to only allow a single `$attributes` parameter via an interface (`\Winter\Storm\Database\ModelInterface` and `\Winter\Storm\Halcyon\ModelInterface`). This will ensure that calls like `Model::make()` or `Model::create()` will execute correctly. It is possible that some people might have used additional parameters for their model constructors - these will no longer work and must be moved to another method.
- The Halcyon Builder `insert` method now returns an `int` representing the created model's filesize, not a `bool`.
- The Halcyon Builder `insert` method requires the `$values` parameter to actually contain variables and will throw an Exception if an empty array is provided. Previously, this was silently discarded and returned `true` (although this would not actually save the file).

<a name="storm-html"></a>
#### HTML

- The `Winter\Storm\Html\FormBuilder` class has had type hinting and return types added to enforce functionality and clarify documentation. If you extend this class in your plugin, you may need to make changes to your method signatures if you overwrite the base functionality.

<a name="storm-parse"></a>
#### Parse

- The `Bracket` class constructor is now `final` to prevent unsafe static calls to the `parse` static method.
- The `Bracket::parseString()` method previously returned `false` if a string was not provided for parsing, or the string was empty after trimming. Since the signature calls for a string, we won't check for this anymore. If the string is empty, an empty string will be returned.
- The `markdown.beforeParse` event in the `Markdown` class sent a single `MarkdownData` instance as a parameter to the listeners. It now sends an array with the `MarkdownData` instance as the only value, to meet the signature requirements for events.
- The `Syntax\FieldParser` class constructor has been made `final` to prevent unsafe static calls to the `parse` statuc method.
- The `$template` parameter for the `Syntax\FieldParser` class constructor was originally optional. Since there is no purpose for this, and no way to populate the template after the fact, this has been made required.
- The `Syntax\Parser` class constructor has been made `final` to prevent unsafe static calss to the `parse` static method.
- The `$template` parameter for the `Syntax\Parser` class constructor was originally optional. Since there is no purpose for this, and no way to populate the template after the fact, this has been made required.

<a name="storm-support-testing"></a>
#### Support\Testing

- The `Winter\Storm\Support\Testing\Fakes\MailFake::queue()` method has had its signature re-arranged to remain compatible with Laravel's `MailFake` class, with the `$queue` parameter being moved to the second parameter. The new signature is `($view, $queue, $data, $callback)`.



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
