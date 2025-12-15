---
title: Movable Type で「Can't call method "type" on an undefined value」エラーが発生した時の対処
date: "2021-03-15T05:37:00.000Z"
description: 'Movable Typeで「Can''t call method "type" on an undefined value」というエラーが出る原因（の一つ）'
---

ローカル環境で構築したサイトをエクスポートして別環境にインポートしたところ再構築時に `Can't call method "type" on an undefined value` というエラーが出るようになった。

これだけでは何処の何が原因でエラーが発生しているのか分からないので、テンプレートを一つずつ再構築したりテンプレートタグをコメントアウトしてみたりという原始的な方法で原因箇所を特定した。

結論から言うと `MTContents` タグの `field:` モディファイアにコンテンツフィールドのユニークIDを指定していた事が原因だった。

https://www.movabletype.jp/documentation/appendices/tags/contents.html

> 日本語や半角空白が含まれるコンテンツフィールドの場合は、field: の後ろに指定することはできませんのでユニーク ID を代わりに指定します。

とあるが

https://www.movabletype.jp/faq/server-migration.html

> インポートするとサイトの ID やコンテンツタイプのユニーク ID などが変わるため、テンプレート内の ID / ユニーク ID 指定部分があれば書き換える必要があります。

という罠があった。（ちゃんとドキュメント読め）

回避策として DB を直接 dump & restore して移行する方法があるが、直接 DB を触れる環境ではなかったので今回は使えなかった。

今後新しく環境作ったりでインポートする度に変更するのは面倒だしまたハマりそうな気がするので結局今回はフィールド名を英字にする事にした。
