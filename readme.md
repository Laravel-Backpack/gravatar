# Gravatar for Laravel 12 & 13

[![Total Downloads](https://poser.pugx.org/backpack/gravatar/d/total.svg)](https://packagist.org/packages/backpack/gravatar)
[![Latest Stable Version](https://poser.pugx.org/backpack/gravatar/v/stable.svg)](https://packagist.org/packages/backpack/gravatar)
[![License](https://poser.pugx.org/backpack/gravatar/license.svg)](https://packagist.org/packages/backpack/gravatar)

> NOTE: This is a fork of https://github.com/brainpink/gravatar. We had to fork it, to add Laravel 13 support. All the work is credited to the maintainers of that package. 

## Installation

First, pull in the package through Composer via the command line:
```js
composer require backpack/gravatar
```

or add the following to your composer.json file and run `composer update`.

```js
"require": {
    "backpack/gravatar": "~1.0"
}
```


Finally, publish the config by running the `php artisan vendor:publish` command


## Usage

Within your controllers or views, you can use

```php
    Gravatar::get('email@example.com');
```

this will return the URL to the gravatar image of the specified email address.
In case of a non-existing gravatar, it will return return a URL to a placeholder image. 
You can set the type of the placeholder in the configuration option `fallback`. 
For more information, visit [gravatar.com](https://docs.gravatar.com/api/avatars/images/#default-image)

Alternatively, you can check for the existence of a gravatar image by using

```php
    Gravatar::exists('email@example.com');
```

This will return a boolean (`true` or `false`).

Or you can pass a url to a custom image using the fallback method:

```php
    Gravatar::fallback('http://urlto.example.com/avatar.jpg')->get('email@example.com');
```


## Configuration

You can create different configuration groups to use within your application and pass the group name as a second parameter to the `get`-method:

There is a default group in `config/gravatar.php` which will be used when you do not specify a second parameter.

If you would like to add more groups, feel free to edit the `config/gravatar.php` file. For example:

```php
return array(
	'default' => array(
		'size'   => 80,
		'fallback' => 'mm',
		'secure' => false,
		'maximumRating' => 'g',
		'forceDefault' => false,
		'forceExtension' => 'jpg',
	),
	'small-secure' => array (
	    'size'   => 30,
	    'secure' => true,
	),
	'medium' => array (
	    'size'   => 150,
	)
);
```

then you can use the following syntax:

```php
Gravatar::get('email@example.com', 'small-secure'); // will use the small-secure group
Gravatar::get('email@example.com', 'medium'); // will use the medium group
Gravatar::get('email@example.com', 'default'); // will use the default group
Gravatar::get('email@example.com'); // will use the default group
```

Alternatively, you could also pass an array directly as the second parameter as inline options. So, instead of passing a configuration key, you pass an array, which will be merged with the default group:

```php
Gravatar::get('email@example.com', ['size'=>200]); 
```

