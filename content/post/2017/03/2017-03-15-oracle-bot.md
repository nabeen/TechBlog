+++
tags = ["bot", "oracle", "event"]
slug = "oracle-bot"
categories = ["bot"]
thumbnail = ""
date = "2017-03-15T20:41:34+09:00"
description = ""
title = "オラクルで開催されたBotの勉強会に参加してきた！"
author = "nabeen"
draft = false

+++

今日はオラクルさんで開催された[社食で働くBotの働きぶりをデモで鑑賞しつつ、Bot本体の構造と開発メソッドを詳しく学ぶ会@福岡 \- Oracle Cloud Developers 九州 \| Doorkeeper](https://oracleclouddevelopersq.doorkeeper.jp/events/58032)に参加してきました！今週はpixivにも行けるし、楽しい一週間です。

内容としては、まぁDoorkeeperのタイトルのまんまですが、実際にオラクル社内で使われているBotの機能面、技術面についての話がありました。

なお、本日のスライドは以下になりますmm

[Waterfall cafeで働くBot](https://www.slideshare.net/nkjm/waterfall-cafebot)

## Botの概要
LINE、Facebook Messenger上で稼働しているBotで、機能としては以下の3つ。

* 今日のメニュー/カロリー
* 社内のFAQ機能
* カフェの照明調整

自然言語処理を入れていて、従来型？の正規表現ゴリゴリみたいなのとは違うくて、柔軟な処理(より会話に近い処理)ができるようになっているとのことです。

## Botのアークテキチャ
詳しい部分は本日の資料なり、[AIが入ったBotを高速開発するフレームワーク：bot\-expressの概要と使い方 \- Qiita](http://qiita.com/nkjm/items/858b7e4a65eb2ebbaf65)の記事を読んだ方が早いですね。

本体はNodeJSでnpmで配布されているので、僕も実際に使える！わっほい！

一番興味のあった自然言語処理については、[Conversational UX Platform for products and services \- API\.AI](https://api.ai/)を使っているんだそう。こんなのあるんや、、知らなかった。Googleが買収したんですね。

## Botを作る時のポイント(アプローチ面)
「使えるモノは使う」で開発するのが捗るそうです。いわゆるマッシュアップで作れってことかな？

でも僕はお金もないしスキルも磨きたいので、基本的には自前でやっていきたい派です。まぁ確かに業務で作るんだったらより楽な方に進みたい気持ちもあるけど、個人的に勉強としてやるんだったら、イバラの道をあえて進んだほうがいいですしね。

## Botを作る時のポイント(実装面)
えいやで作ると結構ごちゃっとしてすぐスパゲティになるので、今回作ったFW、[nkjm/bot\-express: Chat Bot builder framework based on flow and skill model](https://github.com/nkjm/bot-express)では、役割をハッキリ分けて対応しているそうです。

### スキル
* Botができる仕事
* これを簡単に追加したい

### フロー
* 文脈に応じてどういう順番に何を実行するか
* ここの結果いかんでBotのスケーラビリティーが変わる

まぁユーザーからのデータ(発言)を上手にフロー側の処理で分岐させて、処理対象のスキルをフックさせる感じかな？話を聞いた限りでは。実際にどういう処理を噛ませばいいかってのは今日の勉強会では話がなかったので、あとは勝手にソースを読めと( ˘ω˘)ｽﾔｧ

NodeJS、、僕の苦手分野です。

## おわりに
PythonのSlack botを簡単に作りたいんだけど誰か良いFW教えてくれないかなーServerless Frameworkでもできそうなんだけど結構みんなNodeJSなんだよなーbot界隈はNodeJS大好きなのかなー、つらみ。

それでは良きBotライフを！
