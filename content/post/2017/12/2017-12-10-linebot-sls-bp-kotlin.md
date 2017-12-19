+++
title = "LINE BOTをKotlinで書く為の雛形、linebot-sls-bp-kotlinを公開しました #app_a_week"
slug = "linebot-sls-blueprint-kotlin"
description = ""
date = "2017-12-10T12:00:00+09:00"
categories = ['Kotlin', 'App A Week']
tags = ['Kotlin', 'LINE BOT']
thumbnail = ""
author = "nabeen"
+++

先週に引き続きKotlinネタです。今週はやる気が無かった（）ので、軽めの実装です。先週作ったモノから一部を切り出して、これからKotlinでLINE BOTを作る人向けの雛形として、`linebot-sls-bp-kotlin`を公開しました。

GitHubはこちら▼

[nabeen/linebot\-sls\-bp\-kotlin: based on https://github\.com/moritalous/linebot\-serverless\-blueprint\-java](https://github.com/nabeen/linebot-sls-bp-kotlin)

基本的には各々のキーのみ設定すればいいように実装しています（したつもりです）。

## Idea

先週KotlinでLINE BOTを作った時、KotlinでLINE BOTを実装している人の少なさに絶望しました。

そして、Kotlin初心者（Javaも書いたこと無い）の僕が果たしてKotlinで実装出来るんだろうか...と不安になりました。

基本的に**サクッと作れてサクッとうぇーい出来ること**が新しい技術を学ぶ時の最低限のハードルだと思います。例えば「すごい技術だけど環境構築がつらみある」とかだと、なかなか最初の一歩が踏み出せないですよね。

なので、これからKotlinでうぇーいしたい人の為に、サクッと設定してサクッと動かせる雛形として、`linebot-sls-bp-kotlin`を公開しました。

※尚、本実装は、[moritalous/linebot\-serverless\-blueprint\-java: linebot\-serverless\-blueprint\-java](https://github.com/moritalous/linebot-serverless-blueprint-java)の実装を非常に参考にしています。

## What went right

### Kotlinのシンタックスに対する理解が少し深まった

先週実装した時は、「とりあえず動けばいい」で実装したので、Kotlinぽい実装は全く意識していませんでした。

ただ今回雛形として作るにあたっては、「少しでもKotlinぽいモノ」にしたかったので、**IntelliJ IDEAの機能を駆使して**なるべくKotlinぽいモノに近づけようという努力はしました。

例で言えば`when`のシンタックスですね。これはキレイでとても好きです。

```kt
when {
    rawBody != null -> {
        body = rawBody
    }
    objectBody != null -> {
        try {
            body = objectMapper.writeValueAsString(objectBody)
        } catch (e: JsonProcessingException) {
            LOG.error("failed to serialize object", e)
            throw RuntimeException(e)
        }
    }
    binaryBody != null -> {
        body = String(Base64.getEncoder().encode(binaryBody!!), StandardCharsets.UTF_8)
    }
}
```

## What went wrong

**テストまだ書いてません**。いつものことですが！

あとは`gradle`周りがよくわからず、最新verだったら動かなかったとか...。

とりあえずver落とせば動いたので公開はしましたが、`gradle`周りの謎はまだ解けてません。いつか、いつかきっと解決します₍₍⁽⁽(\(*ﾟ▽ﾟ*)ʃ)₎₎⁾⁾ノリノリ！

## What I learned

既出ですが、箇条書きとしてまとめます。

- Kotlinぽい書き方に近づけたれた
- 公開前提で書くと色々気を使う
- やる気の出ない時は過去にやったプロジェクトをOSSとして切り出すのは、アリ

## 参考サイト

- [moritalous/linebot\-serverless\-blueprint\-java: linebot\-serverless\-blueprint\-java](https://github.com/moritalous/linebot-serverless-blueprint-java)
