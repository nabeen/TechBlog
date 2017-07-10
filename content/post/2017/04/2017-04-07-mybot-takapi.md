+++
draft = false
tags = ["Bot", "Hubot", "Node.js", "CoffeeScript"]
author = "nabeen"
thumbnail = ""
categories = ["Bot"]
date = "2017-04-07T22:07:01+09:00"
description = ""
slug = "mybot-takapi"
title = "今更ながらSlack内にHubotを召喚してみました"

+++

最近社内でChatOps、DevOps周りに取り組んでいます。

せっかくなので、個人で使っているSlackにも導入しようと思い立ちまして。今僕のSlackにはBotが常駐しています。`heroku-keepalive`がうまく動いてない気がしますが。。。

[![https://gyazo.com/f93c152a1100ac7e3fedbaeda6841630](https://i.gyazo.com/f93c152a1100ac7e3fedbaeda6841630.png)](https://gyazo.com/f93c152a1100ac7e3fedbaeda6841630)

### Hubotの作成方法
詳細はもう色んな所で出回っていますので、割愛します。サーバーは大好きなHerokuを使います。

* Slack側でHubotの設定をする
* Hubot公式を見て写経する
* Herokuでアプリを作る
* デプロイ(push)する
* 環境変数(トークン、タイムゾーン等)

Hubot公式はこちら。

[HUBOT](https://hubot.github.com/docs/)

ちなみに、現状の成果物はこちらです。今ちょっとだけやる気なので、随時更新していきます。

[nabeen/takapi: 嫁の名を冠したbotです\(Hubot\)](https://github.com/nabeen/takapi)

### CoffeeScript？
HubotはCoffeeScriptで書くのが一般的なようです。でも、JavascriptでもOK。

ということで、上記の僕の成果物には、ES6でも書けるようにBabelを入れています（会社でも同じことをやってる）。ただ、現状で僕のJS力が全く無いので、ES6の記法が全くわからない／(^o^)＼という壁にぶつかっています。だからExpressに入門してるんですけどね。。

[Node\.jsならexpressと聞いてHello Worldまでやってみた](https://nabeen.github.io/2017/04/07/hello-express/)

そして今日、Node.jsならES5に変換しなくても大丈夫って情報を得たんですが、本当でしょうか。。分かり次第、追記します^^;

### このBotで実現したいこと
Siriっぽくしたいんですよね、Siri。機械学習的な、人工知能的な。

「機械学習やります！」って言ってからほぼ何もしてないし、まぁBotと絡めてやったら楽しみながらできそうかな？っていう目論見。その前に、JS力とかHubot力を上げておきたい所存。

機械学習だとさすがにJSだとつらいから、PythonのAPIサーバーでも立ててHubotからコールするとかが良いかもですね。あれ、それってつまりPythonのフレームワークも勉強しないとなんじゃ。。Expressじゃなくて、こっちのほうが優先やな。。つらみ。

Pythonのフレームワークって、、軽いのだとFlaskとか？

まぁ、考えます。

それでは良きHubotライフを！
