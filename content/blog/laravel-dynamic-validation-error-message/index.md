---
title: Laravel のバリデーションエラーメッセージに動的に値を埋め込む
date: "2022-05-24T09:07:00.000Z"
description: "Laravel のバリデーションエラーメッセージに動的に値を埋め込む方法"
---

attribute とか parameters ではなくバリデーションの過程で得られる情報をエラーメッセージに埋め込みたかった。

## 実装例
カンマ区切りの数値形式の文字列である事を検証するカスタムバリデーションルールで数値形式の文字列じゃなかった値をエラーメッセージに埋め込む。

```php
<?php

namespace App\Rules;

use Illuminate\Contracts\Validation\Rule;
use Illuminate\Contracts\Validation\ValidatorAwareRule;
use Illuminate\Validation\Validator;

class CommaSeparatedNumeric implements Rule, ValidatorAwareRule
{
    protected Validator $validator;

    /**
     * @param Validator $validator
     * @return $this
     */
    public function setValidator($validator): self
    {
        $this->validator = $validator;
        return $this;
    }

    /**
     * @param string $attribute
     * @param mixed $values
     * @return bool
     */
    public function passes($attribute, $values)
    {
        foreach (explode(',', $values) as $value) {
            if (!is_numeric($value)) {
                $this->validator->addReplacer(
                    self::class,
                    fn($message) => str_replace(':value', $value, $message)
                );
                return false;
            }
        }
        return true;
    }

    public function message(): string
    {
        return ':attribute must be comma separated numeric. (:value is not numeric)';
    }
}
```

- `ValidatorAwareRule` を実装して Rule クラス内から `Validator` に触れるようにする。
- `Validator::addReplacer()` で動的にエラーメッセージの Replacer を追加する。

## 実行例
```
>>> use App\Rules\CommaSeparatedNumeric
>>> Validator::make(['input' => '1,2,3'], ['input' => new CommaSeparatedNumeric()])->validate()
=> [
     "input" => "1,2,3",
   ]

>>> Validator::make(['input' => '1,2,3,a,b,c'], ['input' => new CommaSeparatedNumeric()])->validate()
Illuminate\Validation\ValidationException with message 'input must be comma separated numeric. (a is not numeric)'
```

この例だったら最初から配列に変換しておけ感はある。
