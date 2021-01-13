---
title: うっかり消した vendor/bin/sail を復元する
date: "2020-12-23T00:00:00Z"
description: "うっかり消した vendor/bin/sail を復元する方法"
---

Laravel Sail をいじってる最中、最適化したらどのくらいパフォーマンス出るんだろうな～と何も考えずに以下のコマンドを実行

```bash
$ sail composer install --no-dev
（中略）
  - Removing laravel/sail (v0.0.9)
```

（あっ）

```bash
$ sail composer install
zsh: no such file or directory: ./vendor/bin/sail
```

という訳で[公式ドキュメント](https://laravel.com/docs/8.x/sail#installing-composer-dependencies-for-existing-projects)に助けを求める。
> You may install the application's dependencies by navigating to the application's directory and executing the following command. This command uses a small Docker container containing PHP and Composer to install the application's dependencies

```bash
$ docker run --rm \
    -v $(pwd):/opt \
    -w /opt \
    laravelsail/php80-composer:latest \
    composer install
```

これで無事にインストールし直せた。

---

ちなみにローカルに composer がインストールされていて `composer install` できればそれに越した事はない。（自分の環境では PHP のバージョン不一致で失敗した）
