[![Latest Stable Version](https://poser.pugx.org/mprince/laravel7-pointable/v/stable)](https://packagist.org/packages/mprince/laravel7-pointable)
[![Total Downloads](https://poser.pugx.org/mprince/laravel7-pointable/downloads)](https://packagist.org/packages/mprince/laravel7-pointable)
[![Latest Unstable Version](https://poser.pugx.org/mprince/laravel7-pointable/v/unstable)](https://packagist.org/packages/mprince/laravel7-pointable) 
[![License](https://poser.pugx.org/mprince/laravel7-pointable/license)](https://packagist.org/packages/mprince/laravel7-pointable)

# Laravel Pointable

Point Transaction system for Laravel 7.*

Inspired from [Trexology](https://github.com/Trexology/laravel-pointable)

## Installation

First, pull in the package through Composer.

## For Laravel 8

```js
composer require mprince/laravel-pointable
```

## For Laravel 7

```js
composer require mprince/laravel7-pointable
```

And then include the service provider within `app/config/app.php`.

```php
'providers' => [
    Mprince\Pointable\PointableServiceProvider::class
];
```

At last you need to publish.
```
php artisan vendor:publish --provider="Mprince\Pointable\PointableServiceProvider"
```

and then run the migration.

```
php artisan migrate
```

-----

### Setup a Model
```php
<?php

namespace App;

use Mprince\Pointable\Contracts\Pointable;
use Mprince\Pointable\Traits\Pointable as PointableTrait;
use Illuminate\Database\Eloquent\Model;

class User extends Model implements Pointable
{
    use PointableTrait;
}
```

### Add Points
```php
$user = User::first();
$amount = 10; // (Double) Can be a negative value
$message = "The reason for this transaction";

//Optional (if you modify the point_transaction table)
$data = [
    'ref_id' => 'someReferId',
];

$transaction = $user->addPoints($amount,$message,$data);

dd($transaction);
```

### Subtract Points
```php
$user = User::first();
$amount = 10; // (Double) Can be a negative value
$message = "The reason for this transaction";

//Optional (if you modify the point_transaction table)
$data = [
    'ref_id' => 'someReferId',
];

$transaction = $user->subPoints($amount,$message,$data);

dd($transaction);
```

### Get Current Points
```php
$user = User::first();
$points = $user->currentPoints();

dd($points);
```

### Get Transactions
```php
$user = User::first();
$user->transactions;

//OR
$user['transactions'] = $user->transactions(2)->get(); //Get last 2 transactions

dd($user);
```

### Count Transactions
```php
$user = User::first();
$user['transactions_total'] = $user->countTransactions();

dd($user);
```
