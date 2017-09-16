+++
title = "chaliceを使ってオウム返しするLINE BOTを作る"
slug = "chalice-linebot"
description = ""
date = "2017-09-17T00:59:08+09:00"
categories = ["Python"]
tags = ["chalice", "serverless", "AWS", "Lambda"]
thumbnail = ""
author = "nabeen"
+++

以前Slackで動かすbotを作って、Herokuで動かしたりBluemixで動かしたりしてたんですが、Bluemixがイマイチっていうのと、最近流行りのServerlessという技術スタックを使いたいなぁということで、サクッと(実際は結構ハマった)作ってみたので、ご紹介。

Pythonにはまだ慣れていないので、何かもっと良さげな手法があればTwitterなりで教えていただけると幸いです。

## この記事で説明しないこと
- virtualenvとか
- Serverless frameworkとの比較とか
- LINE BOTそのものとか

お手数ですが、上記に関しては別の記事を漁ってください。virtualenvについては以下の記事が非常に参考になります。

[Pythonの仮想環境構築\(2017年版\) pyenvとpyenv\-virtualenvとvirtualenvとvirtualenvwrapperとpyvenvとvenv \- Qiita](http://qiita.com/maskedw/items/aaa2fd7abfd493cf2820)

## 環境構築
まずはクリーンなPythonの環境を作ります。

```bash
$ pyenv virtualenv 3.6.1 chalice-linebot
$ pyenv activate chalice-linebot
```

これでPython 3.6.1で何も入っていないクリーンな環境が出来上がりました。

## 必要なパッケージを入手する
今回はフレームワークにchalice、そしてLINE BOTにline-bot-sdkを使うので、`pip`でサクッと入れます。

```bash
$ pip install chalice
$ pip install line-bot-sdk
```

## chaliceで新規プロジェクトを作成
chaliceにはジェネレータコマンドがあるので、一発で作れます。BOT名は各自自分の好きに付けてください。僕は安定の嫁の名前・ω・

```bash
$ chalice new-project takapi
$ cd takapi
```

## プロジェクト内部を見てみる
雛形としていくつかファイルが作られてますね。

```bash
$ ls -la
total 16
drwxr-xr-x   6 nabeen  staff  204  9 16 23:49 .
drwxr-xr-x  27 nabeen  staff  918  9 16 23:49 ..
drwxr-xr-x   3 nabeen  staff  102  9 16 23:49 .chalice
-rw-r--r--   1 nabeen  staff   37  9 16 23:49 .gitignore
-rw-r--r--   1 nabeen  staff  731  9 16 23:49 app.py
-rw-r--r--   1 nabeen  staff    0  9 16 23:49 requirements.txt
```

ちなみに依存関係のあるライブラリも入ってきたので、現時点で入っているライブラリを見るとこんな感じです。一旦これを`freeze`して`requirements.txt`に吐き出しておきましょう。

```bash
$ pip list
botocore (1.7.12)
certifi (2017.7.27.1)
chalice (1.0.2)
chardet (3.0.4)
click (6.6)
docutils (0.14)
future (0.16.0)
idna (2.6)
jmespath (0.9.3)
line-bot-sdk (1.5.0)
pip (9.0.1)
python-dateutil (2.6.1)
requests (2.18.4)
setuptools (28.8.0)
six (1.10.0)
typing (3.5.3.0)
urllib3 (1.22)
```

Pythonって依存関係のもlistで見れちゃうから、能動的に入れたのか勝手に入ったのかわかりにくくてアレですね...。

## ファイルを作成する
[40行で書ける！ Serverless LINE BOT](https://www.slideshare.net/linecorp/40-serverless-line-bot)で紹介されていたコードをまるっと使わせて頂きます。Channel Access Token、Channel Secretは環境変数から読み出します。

`app.py`はこんな感じ。

```python{.line-numbers}
#!/usr/bin/env python

import os

from chalice import (
    Chalice, Response
)

from linebot import (
    LineBotApi, WebhookHandler
)

from linebot.models import (
    MessageEvent, TextMessage, TextSendMessage
)

from linebot.exceptions import (
    InvalidSignatureError, LineBotApiError
)

app = Chalice(app_name='takapi')

line_bot_api = LineBotApi(os.environ.get("LINEBOT_CHANNEL_ACCESS_TOKEN", ""))
handler = WebhookHandler(os.environ.get("LINEBOT_CHANNEL_SECRET", ""))


@app.route('/callback', methods=['POST'])
def callback():
    signature = app.current_request.headers['X-Line-Signature']
    body = app.current_request.raw_body.decode('utf-8')
    print(body)
    try:
        handler.handle(body, signature)
    except InvalidSignatureError as e:
        return Response({'error': e.message}, status_code=400)
    return Response({'ok': True})


@handler.add(MessageEvent, message=TextMessage)
def handle_text_message(event):
    line_bot_api.reply_message(
        event.reply_token,
        TextSendMessage(text='{}'.format(event.message.text))
    )
```

`.chalice/config.json`はこんな感じで設定します。`LINEBOT_CHANNEL_ACCESS_TOKEN`、`LINEBOT_CHANNEL_SECRET`はLINE BOTの管理画面から自分のやつを使って書き換えてください。

```json{.line-numbers}
{
  "version": "2.0",
  "app_name": "takapi",
  "stages": {
    "dev": {
      "api_gateway_stage": "dev",
      "environment_variables": {
        "LINEBOT_CHANNEL_ACCESS_TOKEN": "foo",
        "LINEBOT_CHANNEL_SECRET": "bar"
      }
    },
    "prod": {
      "api_gateway_stage": "prod",
      "environment_variables": {
        "LINEBOT_CHANNEL_ACCESS_TOKEN": "foo",
        "LINEBOT_CHANNEL_SECRET": "bar"
      }
    }
  }
}
```

## デプロイする
ここまで出来ればデプロイするだけ。

```bash
$ chalice deploy
```

と言いたいところですが、`future`がインスコ出来ねぇ！って怒られます。どハマりしてた時は、このメッセージを完全にスルーしてましたww

```bash
Could not install dependencies:
future==0.16.0
You will have to build these yourself and vendor them in
the chalice vendor folder.

Your deployment will continue but may not work correctly
if missing dependencies are not present. For more information:
http://chalice.readthedocs.io/en/latest/topics/packaging.html
```

こういう系のやつは、`./vendor`配下に入れてあげればchalice側でよしなにやってくれるようなので、ディレクトリを指定して入れてあげます。

詳しくはエラーで出してくれるリンク先を見てください。ただリンク先ではダウンロードしてーうんぬんかんぬんしてますが、別に`pip`でディレクトリ指定してもいけるっぽかったので、こっちの方が楽でいいと思います。

```bash
pip install future -t ./vendor
```

これでデプロイすればOK。

```bash
$ chalice deploy
```

デフォルトはdev環境設定なので、prodに切り替えたい場合は引数を指定してデプロイします。

```bash
$ chalice deploy --stage prod
```

最後にエンドポイントが表示されるので、それをLINE BOT側のHookに設定してあげれば完成です。ハマらなければ余裕でしたね。まぁハマったんだけどね。

## おわりに
API Gateway、Lambda側の設定は一切書いてないんですが、デプロイするだけでその辺をよしなに全てやってくれるってのは、もう楽でしょうがないですね。僕は多分GUIからポチポチやることはもうない...気がします。

今回はオウム返しだけだったので、次回以降はBluemixで動かしてたBOTの機能を移植するつもりです。

1. 挨拶系
1. 時報系

...まぁこれだけなんですが。

### 参考リンク
以下のリンクを参考にさせていただきました。ありがとうございます！

- [40行で書ける！ Serverless LINE BOT](https://www.slideshare.net/linecorp/40-serverless-line-bot)
- [chaliceを使って簡単にPythonでサーバーレスしよう \- Qiita](http://qiita.com/seike460/items/1cd1f85dd2f782a48d6a)
- [AWS Lambda \+ API Gateway \+ Chalice\(Python2\)でLINE BOT \- c\-bata web](http://nwpct1.hatenablog.com/entry/aws-lambda-apigateway-line-bot)
