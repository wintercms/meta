# Build 1.3.0 - Foundation framework upgrade (Laravel 12.x)

Winter CMS is updating its foundation framework to the latest release. As a result, there are some new requirements to run Winter and some code changes required.

From Build 1.3.0 your webserver will require PHP 8.2 or above to use Winter CMS. Websites using PHP 8.0 or 8.1 will still function normally but will no longer be able to receive updates or install the latest version.

There are various code changes that may be required, including code found in plugins and themes, both private and public depending on what features you are utilizing.

* Build 1.3.0 is available as a test update. Stable release date to be announced.

<a name="requirements"></a>
## New Minimum Requirements

<a name="php-version"></a>
### Application Server
- PHP: 8.2+
- Composer: 2.2+
- curl: 7.34.0+

<a name="database-servers"></a>
### Database Servers
- MariaDB 10.3+ ([Version Policy](https://mariadb.org/about/#maintenance-policy))
- MySQL 8.0+ ([Version Policy](https://en.wikipedia.org/wiki/MySQL#Release_history))
- PostgreSQL 10.0+ ([Version Policy](https://www.postgresql.org/support/versioning/))
- SQLite 3.26.0+ (up from 3.8.8)
- SQL Server 2017+ ([Version Policy](https://docs.microsoft.com/en-us/lifecycle/products/?products=sql-server))

<a name="dependencies"></a>
### Dependencies
- Laravel: 12.x
- Carbon: 3.x (required, Carbon 2.x no longer supported)
- PHPUnit: 11.0 (for testing)
- Symfony: 7.x

>**NOTE**: PHP 8.0 and 8.1 are now [unsupported](https://www.php.net/supported-versions.php).

<a name="upgrade-instructions"></a>
## Upgrade Instructions

1. Update the following `composer.json` requirements:
```json
"require": {
    "php": "^8.2",
    "winter/storm": "~1.3.0",
    "winter/wn-system-module": "~1.3.0",
    "winter/wn-backend-module": "~1.3.0",
    "winter/wn-cms-module": "~1.3.0",
    "laravel/framework": "^12.0",
    "wikimedia/composer-merge-plugin": "~2.0.1"
},
"require-dev": {
    "phpunit/phpunit": "^11.0",
    "mockery/mockery": "^1.6",
    "fakerphp/faker": "^1.9.2",
    "squizlabs/php_codesniffer": "^3.2",
    "php-parallel-lint/php-parallel-lint": "^1.0",
    "dms/phpunit-arraysubset-asserts": "^0.5"
},
```

2. Run `composer update`.

3. Review and update your configuration files to match the [latest defaults](https://github.com/wintercms/winter/tree/develop/config).

4. If using PHPUnit for testing, update your `phpunit.xml` configuration to the 10.5+ schema format.

<a name="known-issues"></a>
## Known Issues

The following first-party plugins require updates for compatibility with Winter CMS v1.3:

- **Winter.Builder** - See [PR #71](https://github.com/wintercms/wn-builder-plugin/pull/71)
- **Winter.Docs** - See [PR #24](https://github.com/wintercms/wn-docs-plugin/pull/24)
- **Winter.Search** - See [PR #10](https://github.com/wintercms/wn-search-plugin/pull/10)
- **Winter.Dusk** - See [PR #3](https://github.com/wintercms/wn-dusk-plugin/pull/3)

All other first-party plugins have been tested and confirmed compatible.

<a name="required-changes"></a>
## Required Code Changes

Any required code changes are described below in sections based on related functionality that you may or may not be using. If you are using the described functionality, please review the section and make the required changes.

Only potentially breaking changes are called out in this document. For the full list of all changes, please see the [1.3.0 release note](https://github.com/wintercms/meta/blob/master/release-notes/build-1.3.0.md).

<a name="toc"></a>
## Affected Functionality

If you are using any of the following functionality it's highly recommended that you take a look at the relevant section in this guide and make any required changes to your usage:

- [PHP 8.5 Compatibility](#upgrade-php85)
- [Console Commands](#upgrade-console)
- [Database & Schema](#upgrade-database)
- [Eloquent Models](#upgrade-models)
- [Authentication](#upgrade-auth)
- [Carbon 3](#upgrade-carbon)
- [Rate Limiting](#upgrade-rate-limiting)
- [Storage & Files](#upgrade-storage)
- [Validation](#upgrade-validation)
- [Unit Testing](#upgrade-testing)
- [Configuration Files](#upgrade-config)
- [Storm Library Internals](#upgrade-storm)
- [Using Laravel Packages](#upgrade-laravel-packages)
- [Upgrade Guides](#upgrade-guides)

<a name="upgrade-php85"></a>
### PHP 8.5 Compatibility

PHP 8.5 introduces native `array_first()` and `array_last()` functions that conflict with Winter's helper functions. If you are using these helpers with 2-3 arguments, you must switch to the `Arr` class methods:

**Before (Winter < v1.3)**
```php
$first = array_first($array, function ($value, $key) {
    return $value > 5;
});

$last = array_last($array, function ($value, $key) {
    return $value > 5;
});
```

**After (Winter >= v1.3)**
```php
use Winter\Storm\Support\Arr;

$first = Arr::first($array, function ($value, $key) {
    return $value > 5;
});

$last = Arr::last($array, function ($value, $key) {
    return $value > 5;
});
```

<a name="upgrade-console"></a>
### Console Commands

#### Silent Flag Short Option Removed

Due to Symfony 7.2 changes, the `-s` short option for `--silent` has been removed from asset compilation commands (`mix:compile`, `npm:*`, `vite:*`). Use the full `--silent` flag instead.

**Before (Winter < v1.3)**
```bash
php artisan mix:compile -s
```

**After (Winter >= v1.3)**
```bash
php artisan mix:compile --silent
```

#### Console Command Lazy Loading

The static `$defaultName` property on console commands is deprecated. Use the `AsCommand` attribute instead:

**Before (Winter < v1.3)**
```php
class MyCommand extends Command
{
    protected static $defaultName = 'my:command';
    protected $signature = 'my:command {argument}';
}
```

**After (Winter >= v1.3)**
```php
use Symfony\Component\Console\Attribute\AsCommand;

#[AsCommand(name: 'my:command')]
class MyCommand extends Command
{
    protected $signature = 'my:command {argument}';
}
```

<a name="upgrade-database"></a>
### Database & Schema

#### Column Modifications (Laravel Behavior Preserved)

> **Note**: While Laravel 11 changed column modification behavior to no longer preserve existing attributes, **Winter CMS v1.3 retains the previous behavior**. Existing column attributes (nullable, default, unsigned, etc.) are automatically preserved when using `->change()` unless you explicitly override them. No changes to your existing migrations are required.

#### Floating-Point Column Types

Remove the `$total` and `$places` parameters from `double` and `float` column definitions:

**Before (Winter < v1.3)**
```php
$table->double('amount', 8, 2);
$table->float('amount', 8, 2);
```

**After (Winter >= v1.3)**
```php
$table->double('amount');
$table->float('amount', precision: 53);

// For unsigned, use method chaining:
$table->double('amount')->unsigned();
```

#### Spatial Types

Specific spatial column methods have been replaced with generic ones:

**Before (Winter < v1.3)**
```php
$table->point('coordinates');
$table->polygon('shapes');
```

**After (Winter >= v1.3)**
```php
$table->geometry('coordinates');
$table->geography('coordinates');
$table->geometry('shapes', subtype: 'polygon', srid: 0);
```

#### Schema Inspection Methods

`Schema::getTables()` and `Schema::getTableListing()` now return schema-qualified names by default:

**Before (Winter < v1.3)**
```php
$tables = Schema::getTableListing();
// Returns: ['migrations', 'users', 'posts']
```

**After (Winter >= v1.3)**
```php
$tables = Schema::getTableListing();
// Returns: ['main.migrations', 'main.users', 'main.posts']

// To get unqualified names:
$tables = Schema::getTableListing(schema: 'main', schemaQualified: false);
// Returns: ['migrations', 'users', 'posts']
```

#### Database Expressions

Database expressions no longer support string casting:

**Before (Winter < v1.3)**
```php
$expression = DB::raw('select 1');
$string = (string) $expression;
```

**After (Winter >= v1.3)**
```php
$expression = DB::raw('select 1');
$string = $expression->getValue(DB::connection()->getQueryGrammar());
```

<a name="upgrade-models"></a>
### Eloquent Models

#### UUID Generation

The `HasUuids` trait now generates **UUID v7** (time-ordered) instead of UUID v4 (random):

**To keep using UUID v4:**
```php
use Illuminate\Database\Eloquent\Concerns\HasVersion4Uuids as HasUuids;

class MyModel extends Model
{
    use HasUuids;
}
```

**New default (UUID v7):**
```php
use Illuminate\Database\Eloquent\Concerns\HasUuids;

class MyModel extends Model
{
    use HasUuids;
}
```

#### The `$dates` Property

The `$dates` property has been removed. Use `$casts` instead:

**Before (Winter < v1.3)**
```php
class MyModel extends Model
{
    protected $dates = ['published_at', 'deleted_at'];
}
```

**After (Winter >= v1.3)**
```php
class MyModel extends Model
{
    protected $casts = [
        'published_at' => 'datetime',
        'deleted_at' => 'datetime',
    ];
}
```

<a name="upgrade-auth"></a>
### Authentication

#### Password Rehashing

Laravel 12 introduces automatic password rehashing on login. A new configuration option has been added:

**config/hashing.php**
```php
return [
    // ... existing config ...

    'rehash_on_login' => false, // Set to true to enable automatic rehashing
];
```

#### Custom Password Column Names

If your user model uses a custom password column name, implement the new `getAuthPasswordName()` method:

```php
class User extends Model implements Authenticatable
{
    public function getAuthPasswordName()
    {
        return 'custom_password_column';
    }
}
```

<a name="upgrade-carbon"></a>
### Carbon 3

Carbon 3 is now required. Carbon 2.x support has been removed.

#### Return Type Changes

`diffIn*` methods now return **floats** and can return **negative values** for past dates:

**Before (Carbon 2.x)**
```php
$diff = $date->diffInDays($otherDate);
// Always returned positive integer
```

**After (Carbon 3.x)**
```php
$diff = $date->diffInDays($otherDate);
// Returns float, negative if $date is after $otherDate

// To get absolute value like before:
$diff = abs($date->diffInDays($otherDate));

// Or use the absolute parameter:
$diff = $date->diffInDays($otherDate, absolute: true);
```

See the [Carbon 3 changelog](https://github.com/briannesbitt/Carbon/releases/tag/3.0.0) for full details.

<a name="upgrade-rate-limiting"></a>
### Rate Limiting

Rate limiting classes now accept **seconds** instead of **minutes**:

**Before (Winter < v1.3)**
```php
use Illuminate\Queue\Middleware\ThrottlesExceptions;

// 2 minutes
return [(new ThrottlesExceptions($maxAttempts, 2))];

// GlobalLimit and Limit also used minutes
new GlobalLimit($maxAttempts, 2); // 2 minutes
new Limit($key, $maxAttempts, 2); // 2 minutes
```

**After (Winter >= v1.3)**
```php
use Illuminate\Queue\Middleware\ThrottlesExceptions;

// Convert to seconds (2 minutes = 120 seconds)
return [(new ThrottlesExceptions($maxAttempts, 2 * 60))];

// GlobalLimit and Limit now use seconds
new GlobalLimit($maxAttempts, 120); // 120 seconds
new Limit($key, $maxAttempts, 120); // 120 seconds
```

<a name="upgrade-storage"></a>
### Storage & Files

#### Local Disk Default Root

The default local disk root path has changed:

**Before (Winter < v1.3)**
```
storage/app
```

**After (Winter >= v1.3)**
```
storage/app/private
```

To restore the previous behavior, update `config/filesystems.php`:

```php
'disks' => [
    'local' => [
        'driver' => 'local',
        'root' => storage_path('app'), // Restore old path
    ],
],
```

<a name="upgrade-validation"></a>
### Validation

#### Image Validation

SVG images are no longer allowed by default in image validation rules:

**Before (Winter < v1.3)**
```php
// SVGs were allowed
'photo' => 'required|image'
```

**After (Winter >= v1.3)**
```php
// To explicitly allow SVGs:
'photo' => 'required|image:allow_svg'

// Or using the File class:
use Illuminate\Validation\Rules\File;

'photo' => ['required', File::image(allowSvg: true)],
```

<a name="upgrade-testing"></a>
### Unit Testing

#### PHPUnit 11

PHPUnit 11 is now required for testing. Key changes:

1. **PHPUnit configuration** must use the 10.5+ schema format
2. **Docblock annotations** are replaced with PHP 8 attributes
3. **Data providers** must be static methods

**Before (PHPUnit 9/10)**
```php
/**
 * @dataProvider provideTestData
 * @depends testSomethingFirst
 */
public function testSomething($data)
{
    // ...
}

public function provideTestData()
{
    return [
        ['value1'],
        ['value2'],
    ];
}
```

**After (PHPUnit 11)**
```php
use PHPUnit\Framework\Attributes\DataProvider;
use PHPUnit\Framework\Attributes\Depends;

#[DataProvider('provideTestData')]
#[Depends('testSomethingFirst')]
public function testSomething($data)
{
    // ...
}

public static function provideTestData(): array
{
    return [
        ['value1'],
        ['value2'],
    ];
}
```

#### PHPUnit Configuration

Update your `phpunit.xml` to remove deprecated options and add caching:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="vendor/phpunit/phpunit/phpunit.xsd"
         bootstrap="vendor/autoload.php"
         cacheDirectory=".phpunit.cache"
         colors="true">
    <!-- ... -->
</phpunit>
```

<a name="upgrade-config"></a>
### Configuration Files

Review and update your configuration files to match the [latest defaults](https://github.com/wintercms/winter/tree/develop/config):

#### config/app.php
- Added `previous_keys` configuration for encryption key rotation (uses `APP_PREVIOUS_KEYS` environment variable)
- `debug` value is now cast to boolean

#### config/hashing.php
- Added `rehash_on_login` option (defaults to `false`)

<a name="upgrade-storm"></a>
### Storm Library Internals

Version 1.3 of Winter includes significant refactoring of the Storm library for Laravel 12 compatibility:

#### Database Layer

- **New PDO Layer**: Introduces `Winter\Storm\Database\PDO\Connection` wrapper with driver-specific implementations (MySql, Postgres, SQLite, SqlServer)
- **Connection Classes**: New driver-specific connection classes (`MySqlConnection`, `MariaDbConnection`, `PostgresConnection`, `SQLiteConnection`, `SqlServerConnection`)
- **HasConnection Trait**: Connection logic extracted to `HasConnection` trait
- **Schema Grammars**: New MariaDB-specific grammar; all grammars support `compileChange` method

#### Authentication

- `setUser()` method on Auth Manager now returns `static` (fluent interface)
- Dynamic password column support via `getAuthPasswordName()` method

#### Query Builder

- `paginate()` method accepts optional `$total` parameter
- `searchWhereInternal()` properly handles `Expression` instances

#### Foundation

- `publicPath($path='')` now accepts optional subpath parameter
- Registers Laravel 11's `ContextServiceProvider`
- `$routeMiddleware` property renamed to `$middlewareAliases`

<a name="upgrade-laravel-packages"></a>
### Using Laravel Packages

The version of Laravel has been changed from 9.x LTS to 12.x. If you are using packages made for Laravel you may have to update them to a version compatible with Laravel 12.x.

Common package updates required:

| Package | Winter 1.2 Version | Winter 1.3 Version |
|---------|-------------------|-------------------|
| laravel/cashier | ^14.0 | ^15.0 |
| laravel/passport | ^11.0 | ^12.0 |
| laravel/sanctum | ^3.0 | ^4.0 |
| laravel/telescope | ^4.0 | ^5.0 |
| laravel/dusk | ^7.0 | ^8.0 |
| laravel/scout | ^9.0 | ^10.0 |

<a name="upgrade-guides"></a>
## Upgrade Guides

The following external upgrade guides may be helpful:

### PHP
- [PHP 8.2](https://www.php.net/manual/en/migration82.php)
- [PHP 8.3](https://www.php.net/manual/en/migration83.php)
- [PHP 8.4](https://www.php.net/manual/en/migration84.php)

### Laravel
- [Laravel 10](https://laravel.com/docs/10.x/upgrade)
- [Laravel 11](https://laravel.com/docs/11.x/upgrade)
- [Laravel 12](https://laravel.com/docs/12.x/upgrade)

### Testing
- [PHPUnit 11](https://phpunit.de/announcements/phpunit-11.html)

### Other Dependencies
- [Carbon 3](https://github.com/briannesbitt/Carbon/releases/tag/3.0.0)
- [Symfony 7](https://github.com/symfony/symfony/blob/7.0/UPGRADE-7.0.md)
