# Build 1.1.0 - Foundation framework upgrade (Laravel 6.x LTS)

Release Note 11

Due to overwhelming support from the community, October CMS is updating its foundation framework to the latest Long Term Support (LTS) release. As a result, there are some new requirements to run October and some code changes required.

From the proposed Build 1.1.0 your webserver will require PHP 7.2.9 or above to use October CMS. After this date, websites using PHP 7.0-7.2.8 will still function normally but will no longer be able to receive updates or install the latest version.

There are various code changes that may be required, including code found in plugins and themes, both private and public depending on what features you are utilizing.

Instructions marked with a `√` can be performed immediately to ensure forward compatibility. In other words the change is compatible with all versions of October, now and after the release. It is recommended to make these changes as soon as possible.

* Build 1.1.0 is available as a test update from 16 August 2020. Stable release date to be announced.

## New system requirements: (`√`)

- PHP 7.2 or greater (recommended PHP 7.4)
- SQLite 3.7.11 or greater (recommended SQLite 3.8.8+)

>**NOTE**: The PHP 7.1 branch, and those before it, are now [unsupported](https://www.php.net/supported-versions.php).

## Affected functionality

If you are using any of the following functionality it's highly recommended that you take a look at the relevant section in this guide and make any required changes to your usage:

- [Composer](#upgrade-composer)
- [Configuration files (`/config/*.php`)](#upgrade-config)
- [Environment variables (`.env` files)](#upgrade-env)
- [Server configuration (`.htaccess` files)](#upgrade-server-config)
- [Any packages made for Laravel](#upgrade-laravel-packages)
- [Laravel package auto-discovery](#laravel-package-autodiscovery)
- [Interacting with `Cache` repositories](#upgrade-cache)
- [String based primary keys in models](#upgrade-string-keys)
- [Use of `$guarded` in models](#guarded-in-models)
- [Wildcard event listeners](#upgrade-wildcard-listeners)
- [Catch-all routing](#catchall-routing)
- [Using Carbon directly](#upgrade-carbon)
- [Using Jenssegers\Date directly](#upgrade-jenssegers-date)
- [Using Symfony directly](#upgrade-symfony)
- [Using League\Csv directly](#upgrade-league)
- [Unit Testing](#upgrade-unit-testing)

## Known issues:

- If using RainLab.Translate, ensure you update to v1.6.x (currently unreleased, manually apply [3e31ce](https://github.com/rainlab/translate-plugin/commit/3e31cee945f3cde55cab0ebd0fa278555207302e)) to resolve `Missing required parameters for [Route: ] [URI: en/{slug}].")`

## Testing instructions:

If you would like to help with the upgrade process please make the following changes in your composer.json file and then run `composer update`.

```json
"require": {
    "php": "^7.2",
    "october/rain": "dev-develop as 1.0",
    "october/system": "dev-developer",
    "october/backend": "dev-develop",
    "october/cms": "dev-develop",
    "laravel/framework": "~6.0",
    "wikimedia/composer-merge-plugin": "1.4.1"
},
"config": {
    "preferred-install": "dist",
    "platform": {
        "php": "7.2"
    }
},
```

## Required code changes:

Any required code changes are described below in sections based on related functionality that you may or may not be using. If you are using the described functionality, please review the section and make the required changes.

<a name="upgrade-composer"></a>
### Composer (composer.json)

If you are using composer you will need to make the following changes to your composer.json file:

```json
"require": {
    "php": "^7.2",
    "october/rain": "~1.0",
    "october/system": "~1.0",
    "october/backend": "~1.0",
    "october/cms": "~1.0",
    "laravel/framework": "~6.0",
    "wikimedia/composer-merge-plugin": "1.4.1"
},
"config": {
    "preferred-install": "dist",
    "platform": {
        "php": "7.2"
    }
},
```

>**NOTE:** See the below section on Unit Testing if you also have a `require-dev` section defined in your `composer.json`.

<a name="upgrade-config"></a>
### Configuration files (`config/*` files) (`√`)

Some new configuration files have been made available as part of the Laravel 6 upgrade. You should add these configuration files to your project's `config` folder, and adjust the configuration as necessary. While you're doing that, it is recommended that you review the rest of the configuration files present on GitHub and ensure that your project's copies are up to date as there have been numerous configuration options added over the past year.

  - [`config/auth.php`](https://github.com/octobercms/october/blob/develop/config/auth.php)
  - [`config/develop.php`](https://github.com/octobercms/october/blob/develop/config/develop.php)
  - [`config/hashing.php`](https://github.com/octobercms/october/blob/develop/config/hashing.php)
  - [`config/logging.php`](https://github.com/octobercms/october/blob/develop/config/logging.php)

A [new config option](https://github.com/octobercms/october/blob/develop/config/app.php#L150) has been added to `config/app.php`, `loadDiscoveredPackages`, which controls the loading of packages through Laravel's package discovery system. If you do not provide this through your own `config/app.php` instance, this will default to `false`.

<a name="upgrade-env"></a>
### Environment variables (`.env` files) (`√`)

If you are using `.env` files with a variable that has a `#` inside of an unquoted value; that will now be treated as a comment due to an upgrade to the `phpdotenv` library used for parsing them.

If you have any `#` characters inside of unquoted environment variables please update them to be quoted instead (ex. `DB_PASS=23das#sdfas` must be updated to `DB_PASS="23das#sdfas"`).

Additionally, `putenv()` no longer changes the value returned by calls to `env()` as the `env` helper is now considered read-only. If dynamically changing configuration is required, it is recommended to use Config values instead as they can be dynamically changed with `Config::set()`

>**IMPORTANT:** `.env` files now require any values with spaces in them to be quoted too, it's recommended to just enclose every single value in `.env` with double quotes.

<a name="upgrade-server-config"></a>
### Server configuration (`.htaccess` files)

With the introduction of core support for the `| resize` filter and associated logic, you will need to add the `storage/app/resized` directory as an allowed directory to your server configuration in order to load the resized images produced by that functionality.

`.htaccess` / Apache: Add `RewriteCond %{REQUEST_FILENAME} !/storage/app/resized/.*` to the `### White listed folders` section, below `RewriteCond %{REQUEST_FILENAME} !/storage/app/media/.*`.

`site.conf` / nginx: Add `location ~ ^/storage/app/resized { try_files $uri 404; }` to the `# Let nginx return 404 if static file doesn't exist` section, below `location ~ ^/storage/app/media { try_files $uri 404; }`.

`web.config` / IIS: Add `<add input="{REQUEST_FILENAME}" matchType="IsFile" pattern="^/storage/app/resized/.*" negate="true" />` below `<add input="{REQUEST_FILENAME}" matchType="IsFile" pattern="^/storage/app/media/.*" negate="true" />`

<a name="upgrade-laravel-packages"></a>
### Using any Laravel based packages

The version of Laravel has been changed from 5.5 LTS to 6.x LTS. If you are using packages made for Laravel you may have to go through and update them to a version compatible with Laravel 6.x.

<a name="laravel-package-autodiscovery"></a>
### Laravel package auto-discovery (`√`)

Starting with the Laravel 6 foundation upgrade, October CMS will now default to no longer loading discovered packages through Laravel's [package auto-discovery](https://laravel.com/docs/6.x/packages#package-discovery) service, as this was having the effect of Laravel packages still being loaded and made active even if the plugin using them had been disabled by the user.

This may mean that plugins that were using packages for Laravel but were not explicitly including them in the boot process for the plugin may no longer have access to these packages. Please note that we recommend that plugins do not rely on auto-discovery, and instead bring in the packages and service providers explicitly through the `Plugin.php` file as part of the `register()` or `boot()` processes.

A [new config option](https://github.com/octobercms/october/blob/develop/config/app.php#L150) has been added to `config/app.php`, `loadDiscoveredPackages`, which controls the loading of packages through Laravel's package discovery system. If you do not provide this through your own `config/app.php` instance, this will default to `false`. If you wish to retain the pre-update functionality, you can set this to `true`.

<a name="upgrade-cache"></a>
### Interacting with Cache repositories directly (`√`, when using `now()->addMinutes()`)

Cache TTL (time-to-live) values that are specified as an integer are treated as seconds now, as opposed to minutes, when interacting directly with a cache repository. If you interact with the cache directly, we recommend that you use `DateTime` or `Carbon` instances to define when your data is to expire (ex. `now()->addMinutes(60)` instead of `60`). If you wish to continue using integers, you will need to multiply your integer values by 60 to get the number of seconds.

>**NOTE**: This does not affect the `cms.urlCacheTtl` and `cms.parsedPageCacheTTL` configuration values, which will continue to use minutes.

<a name="upgrade-string-keys"></a>
### String-based primary keys in models (`√`)

If you are using string based primary keys for your models add `protected $keyType = 'string';` to the model class definition to prevent performance optimizations meant for integer key types from negatively affecting your code.

<a name="guarded-in-models"></a>
### Use of `$guarded` in models (`√`)

Due to a recent security patch made in the Laravel framework ([see discussion](https://github.com/octobercms/library/commit/b779df0174454fea203c10d7582465f9ddaf22fb)), if a model uses the `$guarded` property to define attributes that are to be protected from mass assignment; then any attempts to use mass-assignment to populate a property / attribute of the model that does not exist in the database will fail. Example:

```
MyModel extends Model
{
    $guarded = ['id'];

    $someProperty = null;

    public function setSomePropertyAttribute($value)
    {
        $this->someProperty = $value
    }
}
```

Calling `MyModel::create(['someProperty' => 'data']);` would previously have worked, but will not anymore.

> **NOTE:** October does not recommend this pattern. Unless using the `Purgeable` trait, attributes on a model should always correspond directly to the database schema asssociated with that model. It is perfectly acceptable to have public properties on a model that do not correspond to database schema, but avoid abusing methods & functionality designed for model attributes (i.e. attribute getters and setters) as much as possible.

This specifically affected the `October\Rain\Database\Attach\File` model (and by extension, the `System\Models\File` model), which now use the "fillable" attributes property to define the fields available for mass assignment, as opposed to the "guarded" attributes property. If you extend either of these models to provide your own custom File model and wish to have extra fields stored through mass assignment, you will need to copy the [`$fillable` attribute from the `October\Rain\Database\Attach\File` model](https://github.com/octobercms/library/commit/6cd6af6940ca15598ad1bab64e2db4a005d9d38f#diff-b062dfb9a3f1e4c504ad988c977f1b40R34-R47) and place it in your own extension, adding any extra fields that you wish to be fillable as well.

<a name="upgrade-wildcard-listeners"></a>
### Wildcard event listeners: `Event::listen('example.*', $listener);`

The parameters sent to wildcard event listeners in October has changed to match what Laravel has done since 5.4. This was overlooked in the 5.5 update but is being applied now. Going forward all wildcard event listeners will receive the name of the event currently being fired as the first parameter and an array of the event arguments as the second parameter.

Example of old wildcard listener:

```php
Event::listen('*', function ($params) {
    if (Event::firing() === 'some.specific.event') {
        // do stuff with $params
    }
});
```

Example of new wildcard listener:

```php
Event::listen('*', function ($event, $params) {
    if ($event === 'some.specific.event') {
        // do stuff with $params
    }
});
```

<a name="catchall-routing"></a>
### Catch-all routing (`√`)

Changes to the routing in Laravel 6 have resulted in the behaviour of catch-all routes being changed in October CMS. Previously, a catch-all route could be defined with the following:

```
Route::any('{slug}', 'Backend\Classes\BackendController@run')->where('slug', '(.*)?');
```

The definition `{slug}` in Laravel 6 is now considered to be a *required* URL parameter, and will fail with an exception if the router sees an empty parameter. If your plugin uses a similar routing rule, and you would like URLs with an empty parameter to still be routed to your plugin, you must change this definition to be *optional* by suffixing the parameter name with the question mark (`?`) symbol. Eg:

```
Route::any('{slug?}', 'Backend\Classes\BackendController@run')->where('slug', '(.*)?');
```

This can be done immediately for your plugin routes, as optional parameters were already available in Laravel 5.5.

<a name="upgrade-carbon"></a>
### Using Carbon directly

The Carbon library has been upgraded from version 1 to version 2. While this should mostly work with existing code, please [review the upgrade guide](https://carbon.nesbot.com/docs/#api-carbon-2).

<a name="upgrade-jenssegers-date"></a>
### Using Jenssegers/Date directly

The `jenssegers/date` library has been removed from October entirely as most of its functionality is now present in Carbon 2.0. This should mostly work with existing code unless you were referencing it directly, in which case replace any references to `Jenssegers\Date\Date` with `October\Rain\Argon\Date`.

<a name="upgrade-symfony"></a>
### Using Symfony directly

Symfony has been upgraded to version 4 (except for the Yaml subsystem). If interacting directly with it, please [review the upgrade guide](https://github.com/symfony/symfony/blob/master/UPGRADE-4.0.md)

<a name="upgrade-league"></a>
### Using League CSV directly

The CSV package provided by The PHP League has been upgraded from version 8 to version 9. We have made the necessary adjustments to October CMS in order to accommodate this change, however, if you use the library directly or have extended the `ImportModel` and `ExportModel` classes, it is strongly recommended that you [review the upgrade guide](https://csv.thephpleague.com/9.0/upgrading/) as several methods have been dropped or moved.

### Optional changes (`√`)

The following files have been updated for Laravel 6, however, you may continue to use your current version of these files if you wish:

  - [`bootstrap/autoload.php`](https://github.com/octobercms/october/blob/develop/bootstrap/autoload.php)
  - [`index.php`](https://github.com/octobercms/october/blob/develop/index.php)
  - [`artisan`](https://github.com/octobercms/october/blob/develop/artisan)
  - [`.gitignore`](https://github.com/octobercms/october/blob/develop/.gitignore)

<a name="upgrade-unit-testing"></a>
### Unit Testing

If you are running unit testing for October CMS development, you will need to make some changes to your composer.json file and replace the `tests` folder in your installation to get the updates to the unit tests.

**composer.json** changes required:
```json
"require-dev": {
    "phpunit/phpunit": "^8.0|^9.0",
    "fzaninotto/faker": "~1.9",
    "squizlabs/php_codesniffer": "3.*",
    "php-parallel-lint/php-parallel-lint": "^1.0",
    "meyfa/phpunit-assert-gd": "^2.0.0",
    "dms/phpunit-arraysubset-asserts": "^0.1.0"
},
"autoload-dev": {
    "classmap": [
        "tests/concerns/InteractsWithAuthentication.php",
        "tests/fixtures/backend/models/UserFixture.php",
        "tests/TestCase.php",
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
        "phpunit --stop-on-failure"
    ],
    "lint": [
        "parallel-lint --exclude vendor --exclude storage --exclude tests/fixtures/plugins/testvendor/goto/Plugin.php ."
    ],
    "sniff": [
        "phpcs --colors -nq --report=\"full\" --extensions=\"php\""
    ]
},
"extra": {
    "merge-plugin": {
        "include": [
            "plugins/*/*/composer.json"
        ],
        "recurse": true,
        "replace": false,
        "merge-dev": false
    }
}
```

You then need to replace the contents of your project's `tests/` directory with the [`tests/` directory from the repository](https://github.com/octobercms/october/tree/develop/tests).

For maxium compatibility you can also replace your `phpunit.xml` file with the [`phpunit.xml` file from the repository](https://github.com/octobercms/october/blob/develop/phpunit.xml)

## Plugin Unit Tests

If your plugin contains unit tests, you will need to make some adjustments to your unit tests in order to function with the Laravel 6 upgrade.

- All `setUp` and `tearDown` methods in your unit test classes must now have the return type `void` specified to match PHPUnit 8's requirements.
  - Change all `public function setUp()` methods to `public function setUp(): void`.
  - Change all `public function tearDown()` methods to `public function tearDown(): void`.
- The `syntaxCheck` attribute for the `<phpunit>` tag in your `phpunit.xml` file is now deprecated. This should be removed from your `phpunit.xml` file.

In addition to the changes above, note the following deprecations in PHPUnit 8 - these will be thrown as warnings in your unit tests.

- The `@expectedException` group of docblock annotations are now deprecated. Instead, you should call the following methods inside your unit test method, depending on the annotation:
  - @expectedException: `$this->expectException(ClassName::class)`
  - @expectedExceptionCode: `$this->expectExceptionCode(int)`
  - @expectedExceptionMessage: `$this->expectExceptionMessage(string)`
- The `assertInternalType()` method is no longer available. Instead, you should use the `arrayIs[Type]()` methods, where `Type` is the PHP variable type with a capital letter. For example, instead of `assertInternalType('string', ...)`, you should use `assertIsString`, or `assertInternalType('array', ...)` should be `assertIsArray`.
- The `assertContains()` method no longer tests whether strings are inside strings - it now will only detect if an item is contained in an array. If you are using `assertContains()` in this fashion, you should instead use `assertStringContainsString()`.

For more information on deprecations, see the [PHPUnit 8 release notes](https://github.com/sebastianbergmann/phpunit/blob/8.0.0/ChangeLog-8.0.md#800---2019-02-01). Note that although the `assertArraySubset()` method was deprecated, we are still maintaining the method through requiring the `dms/phpunit-arraysubset-asserts` library, so you may continue to use that assertion.

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
- [PHPUnit](https://github.com/sebastianbergmann/phpunit/blob/8.0.0/ChangeLog-8.0.md#800---2019-02-01)
- [League\CSV](https://csv.thephpleague.com/9.0/upgrading/)

### PHP Upgrade Guides (`√`)

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
