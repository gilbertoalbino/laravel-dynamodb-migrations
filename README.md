# Laravel Package: Migrations for DynamoDB 

# Install
* Composer install
```bash 
composer require quankim/laravel-dynamodb-migrations
```

* Install service provider

```php
// config/app.php
    'providers' => [
        ...
        QuanKim\LaravelDynamoDBMigrations\DynamoDBMigrationServiceProvider::class
        ...
    ];
```
* Config DynamoDB
```php
// config/aws.php
    use Aws\Laravel\AwsServiceProvider;
    
    return [
    
        /*
        |--------------------------------------------------------------------------
        | AWS SDK Configuration
        |--------------------------------------------------------------------------
        |
        | The configuration options set in this file will be passed directly to the
        | `Aws\Sdk` object, from which all client objects are created. The minimum
        | required options are declared here, but the full set of possible options
        | are documented at:
        | http://docs.aws.amazon.com/aws-sdk-php/v3/guide/guide/configuration.html
        |
        */
        'credentials' => [
            'key'    => env('AWS_ACCESS_KEY_ID', ''),
            'secret' => env('AWS_SECRET_ACCESS_KEY', ''),
        ],
        'region' => env('AWS_REGION', 'us-east-1'),
        'version' => 'latest',
        'ua_append' => [
            'L5MOD/' . AwsServiceProvider::VERSION,
        ],
        'endpoint' => env('AWS_ENDPOINT', ''),
        'http' => [
            'verify' => false,
        ]
    ];
```

Commands

## Make Model

Makes a new Model with the given MODEL_NAME inside `App\Models` folder, and suggests a `DummyTable` table.

```
php artisan dynamodb:make_model MODEL_NAME
```

In case you want to specify a different table other than `DummyTable`, you can use `--table=TABLE_NAME`. 

```
php artisan dynamodb:make_model MODEL_NAME --table=TABLE_NAME
```

## Migrate

```
php artisan dynamodb:migrate --force
```

You can use `--force` when running in production. Be careful!

```
php artisan dynamodb:migrate --force
```
