---
title: Laravel の日付クラスのデフォルトを CarbonImmutable に変更する
date: "2021-07-16T00:00:00.000Z"
description: "Laravel の日付クラスのデフォルトを CarbonImmutable に変更する方法"
---

[この記事](https://medium.com/@jaketaylor_52917/how-to-use-carbon-2-0s-carbonimmutable-class-in-laravel-5-8-af7e794efbf7) を紹介すれば終わりなんだけど日本語の情報が見当たらなかったので。

`Illuminate\Support\Facades\Date::use` にデフォルト日付クラスを渡せるので ServiceProvider で呼び出してやると良い。
 
```php
<?php

namespace App\Providers;

use Carbon\CarbonImmutable;
use Illuminate\Support\Facades\Date;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    public function register()
    {
        Date::use(CarbonImmutable::class);
    }
}
```

[ide-helper も対応してくれている](https://github.com/barryvdh/laravel-ide-helper/pull/859)のが地味に嬉しい。

