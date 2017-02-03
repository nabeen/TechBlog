+++
draft = true
thumbnail = ""
description = ""
slug = "start-to-use-composer"
tags = ["composer", "php"]
categories = ["Composer"]
date = "2017-02-03T10:02:21+09:00"
title = "Composerでプロジェクトの雛形をつくってみた"
author = "nabeen"

+++

最近業務改善ツールを書く機会があって、もともとLaravel実装で進めてたんですが、なんとなく使い方がわかっちゃったっていうのと、少し期間が開いたのでなんか飽きちゃったってのが重なって、フルスクラッチで書いています。といってもシェルの資産が多いので、ラップするような簡単なものですが。

今回はそれをComposerのライブラリっぽく書いたので、その知見を残しておきます。今までComposerは使うばっかりで作ったことはなかったので、いい勉強になりました。

## 前提条件
以下の状態を前提にしています、あしからず。

1. composer導入済みであること

## composer.jsonの雛形を作成する
雛形は対話式で作ることができます。基本、Enter押すだけでも作れる感じですね。楽ちん楽ちん。※個人情報な部分は一部伏せ字にしています。

```bash
composer init


  Welcome to the Composer config generator



This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [nabeen/algorithm]: nabeen/algorithm
Description []: any algorithm
Author [nabeen <nabeen@hogehoge.com>, n to skip]:
Minimum Stability []:
Package Type (e.g. library, project, metapackage, composer-plugin) []: project
License []: MIT

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]?
Search for a package:
Would you like to define your dev dependencies (require-dev) interactively [yes]?
Search for a package:

{
    "name": "nabeen/algorithm",
    "description": "any algorithm",
    "type": "project",
    "license": "MIT",
    "authors": [
        {
            "name": "nabeen",
            "email": "nabeen@hogehoge.com"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]?
```

これで雛形の完成。吐き出された`composer.json`は以下の通り。

```bash
$ cat composer.json
{
    "name": "nabeen/algorithm",
    "description": "any algorithm",
    "type": "project",
    "license": "MIT",
    "authors": [
        {
            "name": "nabeen",
            "email": "nabeen@hogehoge.com"
        }
    ],
    "require": {}
}
```

ここで`composer install`すればvendorディレクトリが作られます。

```bash
$ composer install
Loading composer repositories with package information
Updating dependencies (including require-dev)
Nothing to install or update
Generating autoload files
```

試しによく使うMonologでも入れてみましょう。

```json
"require": {
    "monolog/monolog": "1.*"
}
```

これでもっかい`composer install`すると、Monologを入れてくれます。
