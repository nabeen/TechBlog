+++
categories = []
date = "2017-02-01T14:43:52+09:00"
description = ""
tags = []
thumbnail = ""
title = "GithubPagesにHugoで作ったサイトをホスティングする"
slug = "githubpages_hugo"

+++

会社の有志メンバーでとあるブログを既にGithubPages✕Hugoで運用してるんですが、最近全然書いてないし使い方も忘れちゃったしってことで、自分用に作って記憶を蘇らせておきます。これを期に個人の技術ブログもGithubPagesに乗り換えようかなぁ。Githubで管理できる恩恵は、デカイ。

<!-- more -->

## この記事で得られるもの
OSX想定なので、そうでない方は適宜読み替えて下さい。ちなみに僕は以前リモート上のLinuxで試したことがありますが、何気にめんどくさかった記憶があります；；

* GithubPagesでホスティング出来るようになる
* Hugoを使って記事を作ることが出来るようになる
* pushするだけで記事を公開することが出来るようになる

## 大まかな手順
まず始めに、ざっくりとした手順を記載しておきます。

1. リポジトリを作成する
1. Hugoで新しいサイト(ブログ)を作る
1. テーマを設定して記事を書く
1. Werckerの設定をしてGithubにPushする
1. 公開です！おめでとうございます！

なんか簡単そうですね！では頑張っていきましょう。

## リポジトリの準備
リポジトリは2つ用意します。1つでもいいんですが、

* [nabeen/blog](https://github.com/nabeen/blog)
* [nabeen/nabeen.github.io](https://github.com/nabeen/nabeen.github.io)

## Hugoを導入する
OSXな方であれば`Homebrew`で入れられるので便利ですね。

```bash
$ brew install hugo
$ hugo version
Hugo Static Site Generator v0.16 BuildDate: 2016-06-06T21:37:59+09:00
```

## Hugoプロジェクトの作成
適当なディレクトリで`hugo new`します。こういうジェネレータで作れる系のプロダクト、非常に好感が持てますね(\(⁰⊖⁰)/)

```bash
$ hugo new site blog
```

ディレクトリ構成はこんな感じ。

```bash
$ cd blog
$ tree ./
./
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes

6 directories, 1 file
```

ここまででブログを書く準備は半分くらい？は整っています！サクサク進みますよ！

## テーマを導入する
テーマは、[Hugo Themes Site](http://themes.gohugo.io/)が公式なので、ここから好きなのGETしましょう。もちろん自作も出来るので、慣れてきたら作るのもあり。ここでは公式の[Mainroad](http://themes.gohugo.io/mainroad/)を使います。

```bash
$ cd themes
$ git clone https://github.com/vimux/mainroad
```

```toml
baseurl = "/"
title = "Mainroad"
languageCode = "en-us"
paginate = "10" # Number of posts per page
theme = "mainroad"
disqusShortname = "" # Enable comments by entering your Disqus shortname
googleAnalytics = "" # Enable Google Analytics by entering your tracking id


[Author]
    name = "John Doe"
    bio = "John Doe's true identity is unknown. Maybe he is a successful blogger or writer. Nobody knows it."
    avatar = "img/avatar.png"


[Params]
    subtitle = "Just another site" # Subtitle of your site
    description = " John Doe's Personal blog about everything" # Description of your site
    opengraph = true
    leftsidebar = false # Move sidebar to the left side if true
    authorbox = true
    post_navigation = true


[Params.widgets]
    search = true # Enable "Search" widget
    recent_articles = true # Enable "Recent arcticles" widget
    categories = true # Enable "Categories" widget
    tags = true # Enable "Tags" widget
```
