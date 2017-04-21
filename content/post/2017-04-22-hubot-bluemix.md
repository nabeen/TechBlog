+++
author = "nabeen"
categories = ["Hubot", "Bluemix"]
date = "2017-04-22T01:45:36+09:00"
description = ""
draft = false
slug = "hubot-bluemix"
tags = ["Hubot", "Bluemix", "Node", "Bot", "IBM"]
thumbnail = ""
title = "Herokuで動かしていたBotをBluemixに移設して無料枠内で運用する"

+++

Bluemixやってますか？

僕は去年アカウントを取ったものの、何をするでもなく無料期間が過ぎていましたww

で、なぜその放置していたBluemixに移設したかというと、まぁたかがbotに僕の大事なHerokuの無料枠が食いつぶされるのを防ぐためです。何を隠そう、Herokuの無料枠内でMastodonを動かしたいのです。なので、その前段としてHerokuで動かしていたBotをBluemixに移設しました。

無料枠内的には多分Bluemix上でMastodon立てた方がいいんだろうけど、さくっと立てて見るには多分Herokuの方が早い、はず。AWSでもいいんだけど、楽したいですからね。時間もないし。

### Bluemixの料金体系
HubotはNode上で動くBotフレームワークなので、これをBluemix上で動かすにはCloud FoundryアプリのSDK for Node.jsを利用して作成することになります。

んで、コイツの無料枠はどれくらいあるのかというと、

[![https://gyazo.com/d3a4d24a794c1a3a86dd236867881782](https://i.gyazo.com/d3a4d24a794c1a3a86dd236867881782.png)](https://gyazo.com/d3a4d24a794c1a3a86dd236867881782)

375GB時間？が無料枠内のようです。よくわからん／(^o^)＼

調べた感じだと、一時間あたりのメモリ量ってとこなのだろうか。256MB割り当てたとしたら、256MB×24時間×30日で約185GB時間ということになるんだと思う。多分ね。違ったらごめんね。

### heroku側のアプリを停止する
停止ボタンぽちーってすればいいかと思ったんだけど、そういうわけにもいかず。停止ボタンがないんですよ。。調べた感じ、サーバー(dyno)を0に設定してあげれば止まるっぽい。サーバーを殺して無理やり止めちゃう感じですね（これなら多分WEB上でも出来ると思う。探せなかったけど）。

```bash
heroku ps:scale web=0 --app APP_NAME
```

これでアクセスしたらエラーが帰ってくるから、多分これで合ってるんだと思う。

```bash
$ curl https://takapi.herokuapp.com/
<!DOCTYPE html>
	<html>
	  <head>
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<meta charset="utf-8">
		<title>Application Error</title>
		<style media="screen">
		  html,body,iframe {
			margin: 0;
			padding: 0;
		  }
		  html,body {
			height: 100%;
			overflow: hidden;
		  }
		  iframe {
			width: 100%;
			height: 100%;
			border: 0;
		  }
		</style>
	  </head>
	  <body>
		<iframe src="//www.herokucdn.com/error-pages/application-error.html"></iframe>
	  </body>
	</html>
```

### Bluemix上にアプリを作成する
この記事のままやればサクッとBluemix上でHubotが動きます。さすが先人、偉大です。

[IBM Bluemixを使って、Slackで動くHubotを構築する手順 \- Qiita](http://qiita.com/Amebayashi/items/ca979ec6f925abc7713f)

流れとしては、

* SDK for Node.jsでアプリを作って、
* cfのCLIツールを入れて、
* APIのエンドポイントの設定をして、
* Bluemixにログインして、
* 環境変数設定して、
* デプロイする

簡単ですね。

デプロイはローカルからやってもいいんですが、HerokuみたくGithub連携もできるんで、masterのPushを検知して勝手にデプロイしてもらうこともできます。

まぁこんな感じの設定です。ぽちぽちするだけで設定できて楽ちん。

[![https://gyazo.com/596e025126ab7d3feeb28781190f3850](https://i.gyazo.com/596e025126ab7d3feeb28781190f3850.png)](https://gyazo.com/596e025126ab7d3feeb28781190f3850)

SlackのIncomming Webhookを使えば通知もしてくれる。便利（デプロイだけでいいんだけどなーと思ったりもする）。

[![https://gyazo.com/68002139bc8f15c9246da03df7100d2a](https://i.gyazo.com/68002139bc8f15c9246da03df7100d2a.png)](https://gyazo.com/68002139bc8f15c9246da03df7100d2a)

### もっと色んなことができる！Bluemixで出来ること
今回はHubotを動かすだけだったのでNodeのアプリを作っただけですが、Bluemixってかなりやれること多いんですよね。。これ、下手に自前でエンジニアコスト掛けてやるより、Bluemix上で多少コストかけてでも人的コストを抑えてサクッとなんかリリースするとか、けっこういいんじゃないでしょうか。まぁさすがに個人で使う場合はそこまで課金できないけど、企業なら、ね。

で、なにが出来るのかというと、

[IBM developerWorks 日本語版 : IBM Bluemix](https://www.ibm.com/developerworks/jp/bluemix/tutorial.html)

こいつを読もう。オフィシャルなドキュメント。完全日本語版だからウレシイ。インフラに苦手意識のある僕はこういうサービス大好きですよ。(ΦωΦ)ﾌﾌﾌ…

### おわりに
Bluemix、改めて使ってみたけど、結構さくっとうぇーい系のことができそうで、個人的には結構マッチするサービスかも。クラウド破産だけはしないように気をつけます。

それでは良きBluemixライフを！
