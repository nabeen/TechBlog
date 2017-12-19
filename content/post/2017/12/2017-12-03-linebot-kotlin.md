+++
title = "LINE BOTを書いた。Kotlinで。 #app_a_week"
slug = "linebot-kotlin"
description = ""
date = "2017-12-03T12:00:00+09:00"
categories = ['Kotlin', 'App A Week']
tags = ['Kotlin', 'LINE BOT']
thumbnail = ""
author = "nabeen"
+++

Amazon Echoが買えないので（）、とりあえずスマートホーム化の足がかりとして、KotlinでLINE BOTを書きました。

GitHubはこちら▼

[nabeen/linebot\-kotlin: based on https://github\.com/moritalous/linebot\-serverless\-blueprint\-java](https://github.com/nabeen/linebot-kotlin)

先人の知識が全然なくて危うく爆死するとこでした（）。KotlinでLINE BOTとかちょっとマイナーすぎたか...。

## Idea

Echo買えないってのはまぁ事実ではあるんですが、スマートホーム=外部からも操作できるってことだと思うので、そのインターフェースとして、LINE BOT書こうかなーとぼんやり思ったのがキッカケです。

Slackとかエンジニア寄りのチャットサービスの方がぶっちゃけ連携はしやすい（し、先人の知恵もある）と思ったんですが、「嫁も使うかもしれない」という可能性があったので、そこは素直にユーザー目線でLINEを選択。

Kotlinを選んだのは完全にKotlin欲にちょうどまみれていたからで、特に深い理由があるわけではありません。情報が少なさ過ぎて後々若干後悔しましたが。

ちなみに本プロジェクトで採用したKotlin、Serverless Framework、どちらも初めましてこんにちは状態でした。あと、Javaも全く書いたことないです:D

## What went right

### 先人に頼り切らない実装が出来た

先述したとおり、「KotlinでLINE BOT書いた」先人が皆無だったので、いつもみたくほぼ丸っと使ってなんとなくうぇーいwwってのが出来ない状態でした。

とはいえさすがにフルスクラッチで書くのは、Kotlinスキル的にも、Serverlessスキル的にも厳しそうだった（時間の制約があるので）ので、Javaで書かれた[moritalous/linebot\-serverless\-blueprint\-java: linebot\-serverless\-blueprint\-java](https://github.com/moritalous/linebot-serverless-blueprint-java)を**非常に参考にしながら**実装しました。

その分、思ったより時間はかかりましたが、「最低限」と思っていた機能はなんとか自力？で実装出来たのは、経験値としては大きかったような気がします。

### IDE強い。こんな強いIDEは初めてだ

KotlinということでIntelliJ IDEA CEを使ったんですが、JavaからKotlinの変換はできるわ、間違いは自動で検出してくれるわで、かなりIDEに頼った部分があります。

生産性という面ではいいんでしょうけど、なんとなく操られてる感が...。

あとは静的型付け言語なんで、ビルドでエラーを検出できるのは単純に安心感がありました。

## What went wrong

えいや！で実装した部分が多々あるので、そのへんは直した方がいいんだろうなーとは思っています。

スマートホーム化は現状ではまだまだなので、後々機能開発する時にリファクタ的なことも出来ればいいなと。

あと当然ですが、**テスト書いてません。**

## What I learned

- 初めてのKotlin
- 初めてのServerless Framework
- 初めての...すいませんもうないです

## 参考サイト

- [moritalous/linebot\-serverless\-blueprint\-java: linebot\-serverless\-blueprint\-java](https://github.com/moritalous/linebot-serverless-blueprint-java)
