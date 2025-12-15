---
title: vim-quickrun のデフォルトだったキーマッピングを手動設定する
date: "2021-05-17T00:00:00Z"
description: "vim-quickrun のデフォルトだったキーマッピングを手動設定する方法"
---

Vim のプラグインを更新したら `<Leader>r` で vim-quickrun が実行できなくなった。

https://github.com/thinca/vim-quickrun/blob/master/doc/quickrun.jax#L1029

> デフォルトのキーマッピング(\<Leader>r)を削除。

とのことなので .vimrc に追記した。

```vim
nnoremap <leader>r :QuickRun<CR>
```
