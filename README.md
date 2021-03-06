# wasabi-storage
<p align="center">
    <br>
    <a href="https://packagist.org/packages/siberfx/wasabi-storage" title="Latest Version on Packagist"><img src="https://img.shields.io/packagist/v/siberfx/wasabi-storage.svg?style=flat-square"></a>
    <a href="https://packagist.org/packages/siberfx/wasabi-storage" title="Total Downloads"><img src="https://img.shields.io/packagist/dt/siberfx/wasabi-storage.svg?style=flat-square"></a>
    <a href="https://github.com/siberfx/wasabi-storage/commits/master" title="Last commit"><img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/siberfx/wasabi-storage"></a>

A [Wasabi](https://wasabi.com/) storage driver for Laravel.

This packages uses the AWS S3 storage driver but changes it to use Wasabi endpoints. It should work exactly the same way and support all the same features.

## Installation

```bash
composer require siberfx/wasabi-storage
```
Add a new disk to your `filesystems.php` config

```php
'wasabi' => [
    'driver' => 'wasabi',
    'key' => env('S3_KEY'),
    'secret' => env('S3_SECRET'),
    'region' => env('S3_REGION', 'eu-central-1'),
    'bucket' => env('S3_BUCKET'),
    'root' => env('S3_ROOT', '/'),
    'endpoint' => env('S3_ENDPOINT'),
    'custom_s3_url' => env('S3_CUSTOM_URL', null), // if you used CDN through a provider like cloudflare, here is the url
],
```

## Usage

```php
$disk = Storage::disk('wasabi');

// list all files
$files = $disk->files('/');

// create a file
$disk->put('avatars/1', $fileContents);

// check if a file exists
$exists = $disk->exists('file.jpg');

// get file modification date
$time = $disk->lastModified('file1.jpg');

// copy a file
$disk->copy('old/file1.jpg', 'new/file1.jpg');

// move a file
$disk->move('old/file1.jpg', 'new/file1.jpg');

// get url to file
$url = $disk->url('folder/my_file.txt');

// Set the visibility of file to public
$disk->setVisibility('folder/my_file.txt', 'public');


// See https://laravel.com/docs/8.0/filesystem for full list of available functionality
```
