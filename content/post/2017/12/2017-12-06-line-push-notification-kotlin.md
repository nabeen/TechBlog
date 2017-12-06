+++
title = "LINE Messaging APIを使って定期的にPushメッセージを送る"
slug = "line-push-notification-kotlin"
description = ""
date = "2017-12-07T00:28:41+09:00"
categories = ['Kotlin']
tags = ['Kotlin', 'Serverless', 'AWS', 'LINE Messaging API']
thumbnail = ""
author = "nabeen"
+++

遅ればせながらLINE BOTを作っています。

構成は、Kotlin + Serverless Framework + AWS Lambda + API Gateway + DynamoDBという感じです。まぁ詳しくはGithubまで。

DynamoDBはまぁ使わなくてもいいんですが、DynamoDBを使ったサンプルしか見つけられず、Kotlinの知識がない状態からフルスクラッチで書くのが少々骨が折れそうだったので、そのまま使わせていただきました。

今回はPushメッセージを実装したよって話。

[nabeen/linebot\-kotlin](https://github.com/nabeen/linebot-kotlin)

## 公式リファレンス

今回はKotlinでの実装になるので、Javaのサンプルを参考にします。

`TextMessage`,`PushMessage`のオブジェクトを作って`LineMessagingServiceBuilder`でゴニョゴニョすればいいみたいです。簡単そうですね。

`to`は個人のIDだったりグループのIDだったりを設定すればよしなにしてくれる様子。devは個人ID、prodはグループIDとかにすれば幸せになりそうです。

参考リンク▼

* [APIリファレンス](https://developers.line.me/ja/docs/messaging-api/reference/#anchor-0c00cb0f42b970892f7c3382f92620dca5a110fc)

サンプルコード▼

```java
TextMessage textMessage = new TextMessage("hello");
PushMessage pushMessage = new PushMessage(
        "<to>",
        textMessage
);

Response<BotApiResponse> response =
        LineMessagingServiceBuilder
                .create("<channel access token>")
                .build()
                .pushMessage(pushMessage)
                .execute();
System.out.println(response.code() + " " + response.message());
```

## システム構成

Serverless FrameworkでAWS Lambda上に構築、scheduleを設定して定期的に叩くようにしています。

scheduleは複数設定もできるし、パラメータも渡せるみたいですね。馴染みのあるcron記法でも書けて、非常に好感が持てます！ただし、cronとは若干異なる部分がある為、まるっとそのまま使えないので要注意。

今回は単純にPush（固定値）を試したかっただけなので、パラメータは渡さずにコードの中で定義して実装してみました。

参考リンク▼

* [Serverless Framework \- AWS Lambda Events \- Scheduled & Recurring](https://serverless.com/framework/docs/providers/aws/events/schedule/)

サンプルコード▼

```yml
functions:
  aggregate:
    handler: statistics.handler
    events:
      - schedule:
          rate: rate(10 minutes)
          enabled: false
          input:
            key1: value1
            key2: value2
            stageParams:
              stage: dev
      - schedule:
          rate: cron(0 12 * * ? *)
          enabled: false
          inputPath: '$.stageVariables'
```

参考リンク▼

* [ルールのスケジュール式 \- Amazon CloudWatch Events](http://docs.aws.amazon.com/ja_jp/AmazonCloudWatch/latest/events/ScheduledEvents.html)
* [Rate または Cron を使用したスケジュール式 \- AWS Lambda](http://docs.aws.amazon.com/ja_jp/lambda/latest/dg/tutorial-scheduled-events-schedule-expressions.html)

サンプルコード▼

```
cron(Minutes Hours Day-of-month Month Day-of-week Year)
```

> すべてのフィールドが必須であり、タイムゾーンは UTC のみです。次の表は、これらのフィールドを示しています。

-9時間を頭のなかで計算して設定しないといけないんですね。タイムゾーンがJSTで設定できないのはつらみある。

## ハマったところ

元々のコードを改変しつつ書いたのでちょっと無駄な部分でハマったところはありますが、基本的にはサラッと書けました。

あと、IDEはIntelliJ IDEAのCEを使ってるんですが、やっぱIDE強えなって思いました・ω・。

## Serverless Framework + Kotlinでの実装

コードはGithubにあるので詳細はそちらを参考にしてください。ここでは要点のみ抜粋しておきます。

上記にあげたJavaのコードをKotlinにただ変換したようなコードです。`try-catch`とか、そのへんはベースにしたコードのまんまパクってる感じ。

```java
private fun push() {
    val textMessage = TextMessage("hello");
    val pushMessage = PushMessage(USER_ID, textMessage);

    val client = LineMessagingServiceBuilder.create(CHANNEL_ACCESS_TOKEN).build()

    try {
        val response = client.pushMessage(pushMessage).execute()
        if (response.isSuccessful) {
            LOG.info(response.message())
        } else {
            LOG.warn(response.errorBody().string())
        }
    } catch (e1: IOException) {
        LOG.error(e1)
    }
}
```

こちらも特殊なのは環境変数を渡す処理くらいなもので、書き慣れたcronライクな構文を用いてscheduleを設定してます。rate構文でこういう条件が書けるかどうかは謎。

```yml
push:
  handler: com.serverless.Handler
  environment:
    CHANNEL_SECRET: ${self:custom.otherfile.environment.${self:provider.stage}.CHANNEL_SECRET}
    CHANNEL_ACCESS_TOKEN: ${self:custom.otherfile.environment.${self:provider.stage}.CHANNEL_ACCESS_TOKEN}
    USER_ID: ${self:custom.otherfile.environment.${self:provider.stage}.USER_ID}
  package:
    artifact: push/build/distributions/push.zip
  events:
    - schedule: cron(0 4 * * ? *)
```

Githubはこちら▼

- [nabeen/linebot\-kotlin](https://github.com/nabeen/linebot-kotlin)
