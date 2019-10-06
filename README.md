# laravel-firebase-auth

Secure your laravel API with Google Firebase Auth

Adding the _Middleware_ to your API will ensure that access is granted only using a valid Bearer Token issues by Goggle Firebase Auth.

## Install

```bash
composer require ds/laravel-firebase-auth
```

Publish the package's config.

```bash
php artisan vendor:publish
```

This will add a firebase.php config file where you need to add you Firebase **Project ID**.

## How to use

There are two ways to use this.

### 1. Lock access without JWT token

Add the _Middleware_ on your _Kernel.php_ file.

```php
\ds\LaravelFirebaseAuth\Middleware\JWTAuth::class,
```

### 2. Lock access and identify the client requester

Add the Service Provider to your config/app.php

```php
ds\LaravelFirebaseAuth\FirebaseAuthServiceProvider::class,
```

Register your new Guard on you AuthServiceProvider.php

```php
$this->app['auth']->viaRequest('firebase', function ($request) {
    return app(\ds\LaravelFirebaseAuth\Guard::class)->user($request);
});
```

Now on you auth.php configure you Guard driver to 'firebase'.

```php
'providers' => [
    'users' => [
        'driver' => 'firebase',
        'model' => \ds\LaravelFirebaseAuth\User::class,
    ],
],
```

TODO: Improve examples

## Support

Feel free to open issues and provide feedback.
