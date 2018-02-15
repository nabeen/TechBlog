+++
title = "Amazon Dash ButtonをIoTボタンとして使ってみた"
slug = "init-amazon-dash-button"
description = ""
date = "2018-02-15T18:18:09+09:00"
categories = ['Node.js']
tags = ['Node.js', 'Amazon Dash Button']
thumbnail = ""
draft = true
author = "nabeen"
+++

昨日社内でIoTをやってみよう！ということで軽いハンズオンをやったので、やったことをメモしておきます。

ラズパイでLチカがメインだったんですが、僕はどうしても**Dash Buttonを押したかった**ので、ラズパイの方は早々に投げ捨てて、Dash Buttonを押しまくってました。

Dash Buttonネタなんて既出もいいとこなんですが、まぁそのへんはご愛嬌。

## Dash Buttonでやったこと

- Chatwork APIを使ってChatworkに投稿する

これだけです。簡単ですね。

## 前準備

- Dash Buttonをセットアップする

まずはDash Buttonをネットに繋がないといけません。やり方は公式サイトに載っているように、アプリからポチポチするだけです。

[Amazon\.co\.jp ヘルプ: スマートフォンでDash Buttonをセットアップする](https://www.amazon.co.jp/gp/help/customer/display.html?nodeId=201746340)

**ただし。**

超重要なんですが、**商品選択をせずに終了**してください。商品選んじゃったら、家に届いちゃうのでww

## 使用したライブラリ

今回は以下のライブラリを使用しました。

[maddox/dasher](https://github.com/maddox/dasher)

よく調べてはいないのですが、メジャーどころは他にもいくつかあるとは思います。ググってサクッと出てきたので、コイツを使ったってだけです。

## やること

- Dash ButtonのMACアドレスを取得して、
- `config/config.json`を設定する

これだけ。いい時代。やり方は`README.md`とかを参考に。

## config.json

参考までに、今回投稿に使った設定ファイルを記載しておきます。各パラメータは各自のものに置き換えてください。今回はAPIリクエストで使いましたが、コマンドとかの実行も出来るので、試してみてください:D

```json
{
  "buttons":[
    {
      "name": "post chatwork",
      "address": "MACアドレス",
      "url": "https://api.chatwork.com/v2/rooms/[投稿する部屋ID]/messages",
      "method": "POST",
      "headers": {"X-ChatWorkToken": "[API KEY]"},
      "json": true,
      "formData": {
        "body" : "₍⁽⁽(\\(*ﾟ▽ﾟ*)ʃ)₎₎⁾⁾ノリノリ！"
      }
    }
  ]
}
```

▼Chatwork APIのドキュメント

[エンドポイント /rooms \- チャットワークAPIドキュメント](http://developer.chatwork.com/ja/endpoint_rooms.html)

## Dash Buttonの使いドコロ

わからんww

HTTPリクエスト飛ばせるので、IFTTTと連携してうにょうにょしたりとかいいかもしれませんね。とりあえず我が家での活用法はまだ全く見えてません（）
