+++
categories = []
date = "2017-02-01T14:43:52+09:00"
description = ""
tags = []
thumbnail = ""
title = "GithubPagesにHugoで作ったサイトをホスティングする"
slug = "githubpages_hugo"

+++

会社の有志メンバーでとあるブログを既にGithubPages✕Hugoで運用してるんですが、最近全然書いてないし使い方も忘れちゃったしってことで、自分用に作って記憶を蘇らせておきます。これを期に個人の技術ブログもGithubPagesに乗り換えようかなぁ。Githubで管理できる恩恵は、デカイ。みんな大好きな草も生やし放題ですしね！？

<!-- more -->

## この記事で得られるもの
Mac想定なので、そうでない方は適宜読み替えて下さい。ちなみに僕は以前リモート上のLinuxで試したことがありますが、何気にめんどくさかった記憶があります；；

* GithubPagesでホスティング出来るようになる
* Hugoを使って記事を作ることが出来るようになる
* pushするだけで記事を公開することが出来るようになる(wercker)

## 大まかな手順
まず始めに、ざっくりとした手順を記載しておきます。

1. リポジトリを作成する
1. Hugoで新しいサイト(ブログ)を作る
1. テーマを設定して記事を書く
1. Werckerの設定をしてGithubにPushする
1. 公開です！おめでとうございます！

なんか簡単そうですね！では頑張っていきましょう。

## リポジトリの準備
リポジトリは2つ用意します。1つでもいいんですが、Hugoそのもの(ビルド前)の管理をするリポジトリと、静的サイトをホストする(ビルド後)の管理をするリポジトリの2つに分けるのが個人的にはオススメ。こっちの方がわかりやすいし、ビルドの設定もすこぶる楽なんで。

* ビルド前用リポジトリ：[nabeen/blog](https://github.com/nabeen/blog)
* ビルド後用リポジトリ：[nabeen/nabeen.github.io](https://github.com/nabeen/nabeen.github.io)

## Hugoを導入する
OSXな方であれば`Homebrew`で入れられるので便利です。それ以外の方はがんばってください・ω・

```
$ brew install hugo
$ hugo version
Hugo Static Site Generator v0.18.1 BuildDate: 2016-12-30T02:12:41+09:00
```

## Hugoプロジェクトの作成
適当なディレクトリで`hugo new`します。こういうジェネレータで作れる系のプロダクト、非常に好感が持てます。好きです、大好きです、結婚して下さい！

```
$ hugo new site blog
```

ディレクトリ構成はこんな感じ。テーマ入れないとすっからかん。

```
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
テーマは、[Hugo Themes Site](http://themes.gohugo.io/)が公式なので、ここから好きなのGETしましょう。もちろん自作も出来るので、慣れてきたら作るのもあり。ここでは公式の[Mainroad](http://themes.gohugo.io/mainroad/)を使います。Theブログって感じ。

```bash
$ cd themes
$ git clone https://github.com/vimux/mainroad
```

プロジェクトルートに`config.toml`を作って、設定自体はデフォルトのをちょちょっとアレンジしてこんな感じでどうでしょう。細かいのは後で変えるんで、とりあえず。

```
baseurl = "/"
title = "mainroad"
languageCode = "ja"
countryCode="ja"
HasCJKLanguage=true
paginate = "10" # Number of posts per page
theme = "mainroad"
disqusShortname = "" # Enable comments by entering your Disqus shortname
googleAnalytics = "" # Enable Google Analytics by entering your tracking id


[Author]
    name = "nabeen"
    bio = "nabeen's true identity is unknown. Maybe he is a successful blogger or writer. Nobody knows it."
    avatar = "https://github.com/nabeen.png"


[Params]
    subtitle = "Just another site" # Subtitle of your site
    description = "nabeen's Personal blog about everything" # Description of your site
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

テーマには一点注意点があって、werckerでビルドする時に、リポジトリに含まれていないとビルドでコケるので、テーマファイル自体を自分のHugoのリポジトリに含めてください。僕は手っ取り早く`.git`ファイルを消しちゃったﾃﾍﾍﾟﾛ。多分ちゃんとデキる系の方はsubmoduleとかを使いこなしていい感じするんだろうな・ω・

## wercker設定ファイルの作成
次はビルド/デプロイ自動化用の設定をしていきます。自動化には[wercker](https://app.wercker.com/)を使う。

プロジェクトルートに`wercker.yml`を作って、こんな感じに設定すればOK。

```
box: debian
build:
  steps:
    - arjen/hugo-build@1.14.1:
      flags: --buildDrafts=false
      theme: mainroad
deploy:
  steps:
    - install-packages:
        packages: git ssh-client
    - leipert/git-push:
        gh_oauth: $GIT_TOKEN
        basedir: public
        repo: nabeen/nabeen.github.io
        branch: master
```

`arjen/hugo-build`の最新版は[こちら](https://github.com/ArjenSchwarz/wercker-step-hugo-build/releases)を参考に最新のバージョンを指定します(HEADだとうまく動かなかった；；)。

## weckerに登録、設定する
wercker自体にはGithubで登録できるので、サクッと登録しましょう。で、管理用のbranchを指定してサクサクっと作って、サクサクっとこんな感じのワークフローを作っちゃいます。deploy側にはGithubで作ったトークンが必要なので、Key-Valueで、GIT_TOKEN-[生成したtoken]を設定します。

[![https://gyazo.com/dd095781f21933a1b928f023949764a4](https://i.gyazo.com/dd095781f21933a1b928f023949764a4.png)](https://gyazo.com/dd095781f21933a1b928f023949764a4)

後はデプロイするだけ！

な、なんかエラーが出たら、、**頑張ってください！！**

## おわりに
久しぶりにHugo触ったけど、まぁまぁ覚えてたり忘れてたり。はてなブログより自由度が高いので、カスタマイズは自由自在ですね！手持ちのアドセンスでも貼ってジャブジャブ儲けよう。

それでは良きHugoライフを！
