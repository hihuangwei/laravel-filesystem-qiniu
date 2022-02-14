# Laravel filesystem Qiniu

[Qiniu](http://www.qiniu.com/) storage for Laravel based on [overtrue/flysystem-qiniu](https://github.com/overtrue/flysystem-qiniu).

[![Sponsor me](https://github.com/overtrue/overtrue/blob/master/sponsor-me-button-s.svg?raw=true)](https://github.com/sponsors/overtrue)

# Requirement

-   Laravel >= 9.0

# Installation

```shell
$ composer require "overtrue/laravel-filesystem-qiniu"
```

# Configuration

1. After installing the library, register the `Overtrue\LaravelFilesystem\Qiniu\QiniuStorageServiceProvider` in your `config/app.php` file:

```php
'providers' => [
    // Other service providers...
    Overtrue\LaravelFilesystem\Qiniu\QiniuStorageServiceProvider::class,
],
```

2. Add a new disk to your `config/filesystems.php` config:

```php
<?php

return [
   'disks' => [
        //...
        'qiniu' => [
           'driver'     => 'qiniu',
           'access_key' => env('QINIU_ACCESS_KEY', 'xxxxxxxxxxxxxxxx'),
           'secret_key' => env('QINIU_SECRET_KEY', 'xxxxxxxxxxxxxxxx'),
           'bucket'     => env('QINIU_BUCKET', 'test'),
           'domain'     => env('QINIU_DOMAIN', 'xxx.clouddn.com'), // or host: https://xxxx.clouddn.com
        ],
        //...
    ]
];
```

# Usage

```php
$disk = Storage::disk('qiniu');

// create a file
$disk->put('avatars/filename.jpg', $fileContents);

// check if a file exists
$exists = $disk->has('file.jpg');

// get timestamp
$time = $disk->lastModified('file1.jpg');

// copy a file
$disk->copy('old/file1.jpg', 'new/file1.jpg');

// move a file
$disk->move('old/file1.jpg', 'new/file1.jpg');

// get file contents
$contents = $disk->read('folder/my_file.txt');

// fetch url content
$file = $disk->getAdapter()->fetch('folder/save_as.txt', $fromUrl);

// get file url
$url = $disk->getAdapter()->getUrl('folder/my_file.txt');

// get file upload token
$token = $disk->getAdapter()->getUploadToken('folder/my_file.txt');
$token = $disk->getAdapter()->getUploadToken('folder/my_file.txt', 3600);

// get private url
$url = $disk->getAdapter()->privateDownloadUrl('folder/my_file.txt');
```

[Full API documentation.](http://flysystem.thephpleague.com/api/)

## :heart: Sponsor me

[![Sponsor me](https://github.com/overtrue/overtrue/blob/master/sponsor-me.svg?raw=true)](https://github.com/sponsors/overtrue)

如果你喜欢我的项目并想支持它，[点击这里 :heart:](https://github.com/sponsors/overtrue)

## Project supported by JetBrains

Many thanks to Jetbrains for kindly providing a license for me to work on this and other open-source projects.

[![](https://resources.jetbrains.com/storage/products/company/brand/logos/jb_beam.svg)](https://www.jetbrains.com/?from=https://github.com/overtrue)

## PHP 扩展包开发

> 想知道如何从零开始构建 PHP 扩展包？
>
> 请关注我的实战课程，我会在此课程中分享一些扩展开发经验 —— [《PHP 扩展包实战教程 - 从入门到发布》](https://learnku.com/courses/creating-package)

# License

MIT
