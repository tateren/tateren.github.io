---
title: laravel-admin のエクスポートにリレーションデータを含める方法
date: "2021-09-30T00:00:00.000Z"
description: "laravel-admin のエクスポートにリレーションデータを含める方法"
---
## 経緯
[Laravel admin | Data export](https://laravel-admin.org/docs/en/model-grid-export#Laravel-Excel%20v3.*)

laravel-admin で Laravel-Excel を使用してデータエクスポートをする際に以下のような ExcelExporter クラスを作る。

```php
<?php

Namespace App\Admin\Extensions;

Use Encore\Admin\Grid\Exporters\ExcelExporter;

class PostsExporter extends ExcelExporter
{
    protected $fileName = 'Article list.xlsx';

    protected $columns = [
        'id' => 'ID',
        'title' => 'title',
        'content' => 'content',
    ];
}
```

ここで Post がリレーション author を持っている時、grid の要領で

```php
    protected $columns = [
        'id' => 'ID',
        'title' => 'title',
        'content' => 'content',
        'author.name' => 'author name',
    ];
```

と書けば出力できるんじゃないかと期待して試してみたが特にそんな事は無かった。

## 正しい実装方法
WithMapping インターフェースを実装して map() をこんな感じにすれば期待する出力が得られた。

ヘッダーは名前だけ指定すれば良いので $columns から $headings に変更している。

```php
<?php

namespace App\Admin\Extensions;

use App\Models\Post;
use Encore\Admin\Grid\Exporters\ExcelExporter;
use Maatwebsite\Excel\Concerns\WithMapping;

class PostsExporter extends ExcelExporter implements WithMapping
{
    protected $fileName = 'Article list.xlsx';

    protected $headings = [
        'ID',
        'title',
        'content',
        'author name',
    ];

    public function map($row): array
    {
        /** @var Post $row */
        return [
            'ID' => $row->id,
            'title' => $row->title,
            'content' => $row->content,
            'author name' => $row->author->name,
        ];
    }
}
```
