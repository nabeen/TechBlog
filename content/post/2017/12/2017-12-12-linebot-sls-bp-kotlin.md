+++
title = "LINE BOT written by Kotlin works on AWS Lambda + API Gateway + DynamoDB, builded by Serverless Framework"
slug = "linebot-sls-bp-kotlin"
description = ""
date = "2017-12-13T02:55:59+09:00"
categories = ['Kotlin']
tags = ['Kotlin', 'LINE BOT', 'Lambda', 'API Gateway', 'DynamoDB', 'Serverless Framework']
thumbnail = ""
author = "nabeen"
+++

この記事は[ボット \(Bot\) Advent Calendar 2017 \- Qiita](https://qiita.com/advent-calendar/2017/bot)の20日目の記事です。

最近はスマートスピーカーの機運が高まってきていますが、BOT勢もまだまだ勢いは衰えていませんよ！！！１

家にいない時に電気消したい？家にいない時にエアコンつけたい？これをやるにはBOTが必要ですよね！ということでそんなBOT開発者の為にLINE BOTを`Kotlin`で実装する為の雛形を作りました。

使用する技術スタックは表題にもありますが、以下の通りです。

- LINE BOT SDK
- Kotlin
- AWS Lambda
- API Gateway
- DynamoDB
- Serverless Framework

## 成果物

Githubで公開していますので、よろしければForkするなりIssues登録するなり好きにしてください:D

- [nabeen/linebot\-sls\-bp\-kotlin](https://github.com/nabeen/linebot-sls-bp-kotlin)

なお、本実装には[moritalous/linebot\-serverless\-blueprint\-java](https://github.com/moritalous/linebot-serverless-blueprint-java)を大いに~~パクっ~~参考にさせていただきました。この場を借りて御礼申し上げます:D

### 出来ること

これからBOT開発をしていく上で最低限必要な以下の機能を実装しています。

- 入力された文字列をオウム返しする
- 定期的にPushメッセージを送信する

入力された文字列によって処理を分岐したければそういうロジックを入れればよし、

定期的に何か別のAPIを叩きたければそういうロジックを書けばよし。

BOTにやらせたい処理って基本的にはどちらかに収束すると思うので、それをサクッと書き始められるような雛形、という位置づけです。

## 作成した経緯

以下の理由から、`Kotlin`でLINE BOT書くしかねぇとなりまして。

- `Kotlin`使ってなんか書きたいけどGUI考えるのめんどくさ(ry => BOT書くしかねぇ
- スマートホーム化=外部ネットワークからリクエストを送りたい => BOT書くしかねぇ
- ~~Amazon Echo全然買えない~~ => BOT書くしかねぇ

ところが、LINE BOTの`Kotlin`実装って**非常に人気がない**んですね。ググってもなかなか情報が出てきませんでした。

**ないなら作ればいいじゃない**ということで、作りました。

## ハマったところ

ハマったところというか、まだわかってないんですが（）

Gradleの最新verは執筆時点で`4.4`なんですが、これでビルドすると設定してる`Handler`が見つからずに`ClassNotFoundException`吐いちゃうんですよね。

```bash
Class not found: com.serverless.Handler: java.lang.ClassNotFoundException
java.lang.ClassNotFoundException: com.serverless.Handler
```

とりあえずバージョン落としてビルドすればなぜか通るので、`2.13`まで落としています。原因わかる方いたら助けてプリーズ。

`build.gradle`
```
task wrapper(type: Wrapper) {
    gradleVersion = '2.13'
}
```

`gradle/wrapper/gradle-wrapper.properties`
```
#Fri Feb 24 00:05:35 JST 2017
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-2.13-all.zip
```

その他に関しては、優秀なIDE（IntelliJ IDEA CE）に助けられながら、多少はKotlinぽい？コードになったのかなぁ...とか思ってます。`Kotlin`ほぼ初見で書いているので、変な部分あれば容赦なく突っ込んでください:D

## 参考サイト

- [moritalous/linebot\-serverless\-blueprint\-java](https://github.com/moritalous/linebot-serverless-blueprint-java)
- [linebot\-serverless\-blueprint\-javaを作った！](https://qiita.com/moritalous/items/af4f05543a1b8817e472)
