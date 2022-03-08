---
title: laravel-admin の grid で number_format
date: "2021-09-02T00:00:00.000Z"
description: "laravel-admin の grid で number_format"
---

laravel-admin の grid で

```php
<?php
$grid->column('int')->display(function($value) {
    return number_format($value);
});
```

`Closure::fromCallable` を使って

```php
<?php
$grid->column('int')->display(Closure::fromCallable('number_format'));
```

PHP8.1 からはこう書けるらしい。

```php
<?php
$grid->column('int')->display(number_format(...));
```

