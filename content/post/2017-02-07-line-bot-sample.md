+++
tags = ["line", "bot", "Message API"]
categories = ["line"]
date = "2017-02-07T21:06:56+09:00"
title = "LINE botの使い方レクチャーが社内であったので参加した"
draft = false
thumbnail = ""
description = ""
author = "nabeen"
slug = "line-bot-sample"

+++

LINE BOT AWARDS、1000万円貰えるってよ。

今日社内でLINE BOTの使い方をレクチャーしてもらったので参加しました。さくっと使えていいですね。個人的にはProgressiveWebAppの通知用にLINE BOTを使うのが胸熱だと思ってます。iOSが早く対応してくれないから...

## 出来たもの
では最初に出来たものから！

[![https://gyazo.com/4e8139b3a4abe61beab7e130a50acfbd](https://i.gyazo.com/4e8139b3a4abe61beab7e130a50acfbd.png)](https://gyazo.com/4e8139b3a4abe61beab7e130a50acfbd)

なんか喋ったら( ﾟ∀ﾟ)o彡°おっぱい！おっぱい！って返してくれるbotです。かわいい・ω・ 友達登録もご自由にどうぞ！（そのうち息、しなくなる可能性があります）

<a href="https://line.me/R/ti/p/%40fsd3725q"><img height="36" border="0" alt="友だち追加" src="https://scdn.line-apps.com/n/line_add_friends/btn/ja.png"></a>

細かい手順は[@skycat\_me](https://twitter.com/skycat_me?lang=ja)が[Lineobot\(messageapi\)を試してみる\-heroku版 \- Qiita](http://qiita.com/skycat_me/items/9f27cbd9354515df744a)に書いてくれてるので丸投げします・ω・

## 作業の流れ
今回はherokuにホストしています。

1. LINE BOTを作る
1. シークレットキーとトークンを入手する
1. `heroku create`する
1. 環境変数にシークレットキーとトークンを突っ込む
1. Pushする(今回はgithubからの自動デプロイで設定)
1. 話しかけて応答してくれればOK！

かーんたん！今回はherokuにホストしたけど、次はLambdaでServerless Frameworkを使いたいいいい。Pythonの勉強にもなるですしお。

### herokuの環境変数追加方法
こんな感じ。備忘録。

```
heroku config:set LineMessageAPIChannelAccessToken={ChannelAccessToken} --app APPNAME
heroku config:set LineMessageAPIChannelSecret={ChannelSecret} --app APPNAME
```

## ソース
ソースはこちらです。

[nabeen/nabeen\_line\_bot: line bot](https://github.com/nabeen/nabeen_line_bot)

元ソースは[@skycat\_me](https://twitter.com/skycat_me?lang=ja)に提供してもらいました。さんくす！

## おわりに
簡単でしたね。簡単簡単。Push APIも使いたいー。

[![https://gyazo.com/4e8139b3a4abe61beab7e130a50acfbd](https://i.gyazo.com/4e8139b3a4abe61beab7e130a50acfbd.png)](https://gyazo.com/4e8139b3a4abe61beab7e130a50acfbd)
