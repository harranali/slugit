[![Dependency Status](https://www.versioneye.com/user/projects/584428be1f3a6d01f2f6f55c/badge.svg?style=flat-square)](https://www.versioneye.com/user/projects/584428be1f3a6d01f2f6f55c)
[![Latest Stable Version](https://poser.pugx.org/harran/slugit/v/stable)](https://packagist.org/packages/harran/slugit)
[![License](https://poser.pugx.org/harran/slugit/license)](https://packagist.org/packages/harran/slugit)

# Slugit
Slugit is a laravel slug generator for eloquent models with support for almost all languages.

## Features
* Generating slugs automatically by simply configuring eloquent models
* Multi language support like English, Arabic, Hindi … etc.
* Configuring the separator character
* Generating unique or none unique slugs

## Installation 
You can install the package via composer by simply running the following command
```shell
$ composer require harran/slugit
```

Then add the service provider to this file `config/app.php`
```php
'providers' => [
    // ...
    Harran\Slugit\SlugitServiceProvider::class
];
```

Final step, publish the config file using the following command
```shell
php artisan vendor:publish
```

##Usage 
To start using the package you need to do one simple step, you need to define in your models which field is your slug field and which field is the source of this slug field, in the case of below example our slug field is `slug` and the source field if `title`.

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;
use Harran\Slugit\SlugService;

class Post extends Model
{
	use SlugService;

	/**
	 * Setting which field is the slug and which field is the source for generating the slug
	 * @return array
	 */
    public function slugSettings(){
    	return [
    		'slug' => 'title'
    	];
    }
}
```

Then every time you create a new post like below, the slug will be generated automatically for you.
```php
$post = new Post([
    'title' => 'some post is here',
]);

$post->save();
```