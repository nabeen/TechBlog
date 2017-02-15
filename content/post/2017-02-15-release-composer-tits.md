+++
categories = ["PHP", "Composer"]
title = "Composerで（ジョークとして）ちゃんと使えるライブラリを作って公開するまでの手順"
thumbnail = ""
date = "2017-02-15T13:25:53+09:00"
tags = ["PHP", "Composer", "Library"]
author = "nabeen"
draft = true
slug = "release-composer-tits"
description = ""

+++

前回で、Composerの基本的な作り方を学んだわけですが、実際に使ってもらえるようなものには至っていない（そもそもそういうつもりがやーつ）ので、今回はジョーク系のライブラリとして愛されるものを作って、実際に公開して恥ずかしくないレベルまで持っていくことを目標に頑張っていきます。

外に出さないようなものであればテストも適当、コードもコピペみたいなもので終わってしまいがちですが、きっちり公開する！と決めたらあれやこれや色々調べながら作っていくことになるので、一度実際に自分で作ってみることをオススメします。

コーディング的には全然恥ずかしくないですが、機能的には恥ずかしいのでPackagistにはあげません（あげられません）；；

## 作ったもの
// ここにGithubのリンク

```php
use nabeen\tits

$tits_en = Tits new('en')
echo $tits_en->say(); // ( ﾟ∀ﾟ)o彡°tits！tits！

$tits_jp = Tits new('jp')
echo $tits_jp->say(); // ( ﾟ∀ﾟ)o彡°おっぱい！おっぱい！
```

これだけです。ね、Packagistにあげれないでしょ。

## Composer.jsonをつくる
`composer init`で対話的にひな形を作ったあとで、以下のように中身を整えます。尚、`composer.json`の中身は、個人的に有名だと思っているFrameworkやLibraryを参考にさせていただきました。

[laravel/laravel: A PHP Framework For Web Artisans](https://github.com/laravel/laravel)

[cakephp/cakephp: CakePHP: The Rapid Development Framework for PHP \- Official Repository](https://github.com/cakephp/cakephp)

[sebastianbergmann/phpunit: The PHP Unit Testing framework\.](https://github.com/sebastianbergmann/phpunit)

[Seldaek/monolog: Sends your logs to files, sockets, inboxes, databases and various web services](https://github.com/Seldaek/monolog)

```json
// ここにコードを貼り付ける
```

## ディレクトリ構造を考える

## 実装する

## PHPUnitでテストを書く

## CIサービスを通して品質を保証する

## 公開用にgh-pagesを作る
Githubの`README.md`だけだと味気ないので、ペライチのページをサクッと作って、これまたCIを通してgh-pagesのブランチにデプロイするようにしていきます。

## 外部プロジェクトから実際に使ってみる
何でもいい（ここではLaravelを利用）んですが、手持ちのプロジェクトの`composer.json`に「俺の」ライブラリを追加して、実際にその挙動を試してみます。
