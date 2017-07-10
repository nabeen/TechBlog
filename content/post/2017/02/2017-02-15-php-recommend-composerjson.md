+++
title = "自作ライブラリを実装するにあたって有名どころのライブラリのComposer.jsonの中身を見る"
author = "nabeen"
tags = ["PHP", "Composer"]
date = "2017-02-15T14:53:10+09:00"
description = ""
thumbnail = ""
categories = ["PHP", "Composer"]
slug = "php-recommend-composerjson"
draft = true

+++

公開できるレベルの自作Composerライブラリを書くにあたって、有名どころのライブラリの`composer.json`を調べたのでそのメモです。`composer init`で生成される雛形って、結構スカスカなんですよね。。なので、自作ライブラリも有名ライブラリをパク、、踏襲していい感じに整えていきます。

## 調査対象ライブラリ
調査対象は、自分で選定するのが面倒だったので爆、[PHP オススメのライブラリ \- Qiita](http://qiita.com/mikakane/items/2719df714df5b3fc6adf)で紹介されていたライブラリに加えて、Framework2つを対象にしています。

* [laravel/laravel: A PHP Framework For Web Artisans](https://github.com/laravel/laravel)
* [cakephp/cakephp: CakePHP: The Rapid Development Framework for PHP \- Official Repository](https://github.com/cakephp/cakephp)

## 設定されている項目
上記で挙げたライブラリでは、以下のパラメータが設定されていました。なので、これを全部網羅して書けば、とりあえず恥ずかしくて死んじゃうことはなさそうです。詳細は[The composer\.json Schema \- Composer](https://getcomposer.org/doc/04-schema.md#version)を参考にするとよさそう。英語だけど。

* name
  * ライブラリの名称。`<vendor>/<name>`で設定する。個人だったら`vendor`はGithubの名前にするのが慣例。
* type
  * とりあえず`library`にしとけばいいと思われる（これがデフォルト）。他には`project`,`metapackage`,`composer-plugin`とかあるけど、僕は多分一生使わないでしょう。
* description
  * ライブラリのdescription。
* version
  * ライブラリのバージョン。基本書かないでいいっぽい。むしろ書くなとすら聞こえる。
* homepage
  * プロジェクトのホームページ。書かなくてもいい。僕はGithubPagesで作る予定なので、作ったら書く。作ったら、書く。
* keywords
  * キーワード。書かなくてもいい。いつ使われるかまでは、、Packagistかな？
* support
  * `email`、`issues`、`forum`、`wiki`、`irc`、`source`、`docs`、`rss`
* license
  * ライブラリのライセンス。
* authors
  * `name`、`email`、`homepage`、`role`
* suggest
* require
* require-dev
* conflict
* bin
* autoload
* autoload-dev
* provide
* extra
* replace
* config
* scripts

## 自作ライブラリのcomposer.json
上記を踏まえて、自作ライブラリの`composer.json`は以下のようになりました。なお、以下は執筆時点最新版なので、最新版を見たい方はGithubまで。

// ここにGithub/composer.jsonのリンク

```json
// ここにcomposer.jsonをはりつけ

```

## おわりに
実際に他のライブラリを見るのは結構な労力がかかりますね、、でも、勉強にはなりました。これで僕の`composer.json`スキルはレベルMaxになった感。うぃーね！

それでは良きComposerライフを。
