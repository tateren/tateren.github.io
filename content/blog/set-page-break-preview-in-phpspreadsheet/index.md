---
title: Phpspreadsheet で表示モードを改ページプレビューに設定する
date: "2022-03-08T03:55:00.000Z"
description: "Phpspreadsheet で表示モードを改ページプレビューに設定する方法"
---

ググっても全然出てこなかったので備忘録

```php
<?php

use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Worksheet\SheetView;

$spreadsheet = new Spreadsheet();
$worksheet = $spreadsheet->getActiveSheet();
$worksheet->getSheetView()
    ->setView(SheetView::SHEETVIEW_PAGE_BREAK_PREVIEW);
```

でOK

[Documentation](https://phpoffice.github.io/PhpSpreadsheet/classes/PhpOffice-PhpSpreadsheet-Worksheet-SheetView.html#method_setView)
