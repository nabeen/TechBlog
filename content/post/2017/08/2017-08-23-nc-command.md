+++
title = "ncコマンドでmemcache内のデータを閲覧する"
slug = "nc-command"
description = ""
date = "2017-08-23T19:20:37+09:00"
categories = ["command"]
tags = ["command", "nc", "memcache", "telnet"]
thumbnail = ""
author = "nabeen"
+++

WEBサービスと言えばcacheがつきものですが、その中身を確認したい場合に使える`nc`コマンド。普段あんまり使わないので、備忘録的に残しておきます。

前回使ったのって、、いつだろう、、。

## ncコマンドで接続する
ncコマンドは優秀なヤツで、結構なことができます。僕は全然使いこなせていないですが。ネットワークエンジニアならきっとバリバリ使っていることでしょう！（妄想

ncコマンド自体については、いい感じの記事がQiitaに上がっていたので貼っておきますね。

[nc コマンド 使い方メモ \- Qiita](http://qiita.com/yasuhiroki/items/d470829ab2e30ee6203f)

今回はいわばtelnet的な使い方をしたかっただけなので、以下のコマンドで対象のサービスに接続します。別に接続先がredisでもなんでも一緒です。

```bash
$ nc localhost 12345
```

※接続先に応じて、ホスト名、ポート番号は適宜変更のこと。

## memcacheの中身を確認する
KVSなので、KEY名ベースです。KEY名はサービス(アプリケーション)側でいい感じに作ってると思うので、対象となるKEY名を指定すればOK。

取得は、

```
get KEY_NAME
```

削除は、

```
delete KEY_NAME
```

簡単。もちろんsetも出来るけど、なかなか直接入れることってあんまりないよね...？これでアプリ側で入れたデータを確認したり消したり自由にできちゃいますね。

ただ、「キャッシュにしかないデータ」というパワーワードを聞いたことがあるので、お取り扱いには要注意。
