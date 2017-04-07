+++
date = "2017-04-07T21:43:20+09:00"
description = ""
author = "nabeen"
draft = false
slug = "hello-express"
title = "Node.jsならexpressと聞いてHello Worldまでやってみた"
categories = ["Node.js"]
thumbnail = ""
tags = ["Node.js", "express"]

+++

最近Hubotを業務で触り始めたこともあって、今まで避けてきたJSが立ちはだかっています。

そこで、Node.jsのデファクトはexpressだという話を小耳に挟んだ(ググった)ので、サクサクっと試してみました。Hello Worldまではジェネレータがやってくれるので、基本僕がやることはほぼありません。きっとここから先が難しいんだ。。

### 成果物
とりあえず出来上がったものがこちらです。

[nabeen/demo\_express: Node\.jsならexpressと聞いて](https://github.com/nabeen/demo_express)

いや、ホント、ジェネレータで作っただけなんですけどね。。。

### Hello Worldまでの行き方
公式、

[Express application generator](http://expressjs.com/en/starter/generator.html)

もしくはこれの日本語訳を上から写経すれば迷うことはありません。

[Express のアプリケーション生成プログラム](http://expressjs.com/ja/starter/generator.html)

僕は日本人なので日本語版で・ω・

ごめんなさい、Hello Worldはこれで終わりです。ジェネレータ叩くだけ...

### 中身を見てみる
とは言ってもさすがにこれだけでは終われないので、中身を見てみます。※`node_modules`はアレなんで抜いてます。

```bash
$ tree -I 'node_modules'
.
├── README.md
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.jade
    ├── index.jade
    └── layout.jade

7 directories, 10 files
```

ちな、`package.json`はこんな感じね。

```json
{
  "name": "demo-express",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "body-parser": "~1.17.1",
    "cookie-parser": "~1.4.3",
    "debug": "~2.6.3",
    "express": "~4.15.2",
    "jade": "~1.11.0",
    "morgan": "~1.8.1",
    "serve-favicon": "~2.4.2"
  }
}
```

ふむふむ、

`www`がサーバーの役目をしててメインの`app.js`を叩く感じかなー。んで`routes`で待ち受けて描画は`views`でやると。で、`view`は名前だけしか聞いたことが無い`jade`ってやつで、こんな書き方なのね。

こっちがレイアウトで、

```jade
doctype html
html
  head
    title= title
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
    block content
```

こっちで継承すると。

```jade
extends layout

block content
  h1 #{title}
  p Welcome to #{title}!!
```

他のテンプレートエンジンみたいに、レイアウトの方に埋め込むわけじゃなくて、逆に継承するんか。ちょっと慣れないかも。記法的にはインデント形式で書けてよさそうやね。てか他のテンプレートエンジンとそんなに変わらん感じかな。

### 今後入れたいもの
そもそも右も左もわかんないんだけど、とりあえずなんか良さ気なプロダクトのコードとか見て、どういう構成で書いてるのか見てみたり、Qiitaで良さ気な記事を漁ってみよう。そうしよう。

せっかくなので、

* PostCSS
* Gulp
* webpack

とか、がっつりモダンなフロントエンドとかに触れてみたいと思ってる。こ、この組み合わせはモダンってことでいいんですよね、、、？

それでは良きNode.jsライフを！
