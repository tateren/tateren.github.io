---
title: Dockerコンテナに標準入力を渡す
date: "2021-01-12T23:54:16Z"
description: "Dockerコンテナに標準入力を渡す方法"
---

ホスト上にある SQL ファイルをコンテナ上の DB に流し込みたい時に何回か調べたのでメモ。

以下のオプションで疑似TTYの割り当てを無効化すれば良い。

## docker コマンドの場合

`-t` オプションを抜く。

```bash
$ docker exec -i container_name mysql -u user_name db_name < foo.sql
```

## docker-compose コマンドの場合

`-T` オプションを追加する。

```bash
$ docker-compose exec -T service_name mysql -u user_name db_name < foo.sql
```
