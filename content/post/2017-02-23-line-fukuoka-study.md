+++
description = ""
draft = false
slug = "line-fukuoka-study"
title = "LINE Developer Meetup in Fukuoka #17 に参加してきた！ #LINE_DM"
thumbnail = ""
tags = ["Event", "LINE", "MachineLearning"]
categories = ["Event"]
date = "2017-02-25T13:55:20+09:00"
author = "nabeen"

+++

LINEの勉強会、最近開催されてなかったようですが、ようやく開催されたので突撃してきました！詳細はこちら→[LINE Developer Meetup in Fukuoka \#17](https://connpass.com/event/49575/)

今回は[第1回 Google来襲:福岡ゲーム業界向けクラウド勉強会@サイバーコネクトツー \- connpass](https://connpass.com/event/51388/)と被っていたのでどっちに行こうか迷ったんですが、絶対機械学習の方がいいだろ！と思ってLINEの方に参加！・ω・

## セッション
以下の2セッションがありました。いいですねー機械学習ですねー。Pythonですねー。

* ご家庭でできる！データ分析を支えるクローリング環境の構築
* リアルタイム画風変換とその未来

Pythonは書きやすいし見やすいしとっても好きなんです（書いたこと無いけど）。これからは一家に一人機械学習エンジニアってくらいの需要は出てくると思うので、今のうちに勉強しておくのです。そうなのです。

以下、勉強会で学んだことを羅列していきます(((((((((((っ･ω･)っ ﾌﾞｰﾝ

## ご家庭でできる！データ分析を支えるクローリング環境の構築
データ分析する？じゃあデータが必要だよねってことで、機械学習やる前の、データを集める部分のお話でした。簡潔に言えば、PythonのScrapy使えばこんな簡単にスクレイピングできるんだぜ！っていう。

スクレイピングの本が欲しくなる内容でした。こういう本があるんですよねー誰か買ってくれないかな-(/ω・＼)ﾁﾗｯ |дﾟ)ﾁﾗｯ

<div class="cstmreba"><div class="booklink-box"><div class="booklink-image"><a href="http://www.amazon.co.jp/exec/obidos/asin/4774183679/kenixi04-22/" target="_blank" ><img src="https://images-fe.ssl-images-amazon.com/images/I/51IiWeYB-7L._SL160_.jpg" style="border: none;" /></a></div><div class="booklink-info"><div class="booklink-name"><a href="http://www.amazon.co.jp/exec/obidos/asin/4774183679/kenixi04-22/" target="_blank" >Pythonクローリング&スクレイピング -データ収集・解析のための実践開発ガイド-</a><div class="booklink-powered-date">posted with <a href="http://yomereba.com" rel="nofollow" target="_blank">ヨメレバ</a></div></div><div class="booklink-detail">加藤 耕太 技術評論社 2016-12-16    </div><div class="booklink-link2"><div class="shoplinkamazon"><a href="http://www.amazon.co.jp/exec/obidos/asin/4774183679/kenixi04-22/" target="_blank" >Amazon</a></div><div class="shoplinkkindle"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01NGWKE0P/kenixi04-22/" target="_blank" >Kindle</a></div><div class="shoplinkrakuten"><a href="https://hb.afl.rakuten.co.jp/hgc/12fd8545.b2d9280e.12fd8546.f36f5475/?pc=http%3A%2F%2Fbooks.rakuten.co.jp%2Frb%2F14559253%2F%3Fscid%3Daf_ich_link_urltxt%26m%3Dhttp%3A%2F%2Fm.rakuten.co.jp%2Fev%2Fbook%2F" target="_blank" >楽天ブックス</a></div><div class="shoplinkrakukobo"><a href="http://hb.afl.rakuten.co.jp/hgc/12fd8545.b2d9280e.12fd8546.f36f5475/?pc=http%3A%2F%2Fbooks.rakuten.co.jp%2Frk%2F017982691c4a3b83a417f0be07bcaf8d%2F%3Fscid%3Daf_ich_link_urltxt%26m%3Dhttp%3A%2F%2Fm.rakuten.co.jp%2Fev%2Fbook%2F" target="_blank" >楽天kobo</a></div>                  	  	  	  	</div></div><div class="booklink-footer"></div></div></div>

### データの提供方法
* ファイルによる提供（静的/動的）
* APIによる提供
* なにも提供されない／(^o^)＼

### 定義
* クローリング：WEBから情報を取得
* スクレイピング：取得したデータを構造化する

### 取得元
* API
* RSS
* 静的HTML
* 動的HTML

当然後者になればなるほど難しい。

APIであれば、（だいたい）Jsonなどの構造化されたデータを取得できるので、楽ちん。RSSは、RSS自体は構造化されているものの、RSSのみで得られる情報量が少ないので追加でクロールしないと有用なデータが取得できない。静的HTMLは作り手によって構造がクソだったりするし、さらに動的になるとSplash、Selenium、PhantomJSなどをゴリゴリ使って頑張らないといけない、つらい。

#### Splashとは
[scrapinghub/splash: Lightweight, scriptable browser as a service with an HTTP API](https://github.com/scrapinghub/splash)

クローラーとサーバーの間に挟んで使うようだ。Splashで解析してクローラーに返すようなイメージ。俺氏、いきなり知らない単語が出てきてビビる。

### クローリングの注意
相手方があることなので、お行儀よくやらないと、不正アクセスとみなされてBANされちゃう恐れも。逆に自分のサイトにお行儀の悪いやつが来たら、すぐBANしちゃいますもんね？

* UAに連絡先を書く
* crawl-delayを適切に

などなど。

また、考えなければいけないこととして、以下のようなものもある。

* パフォーマンス
* リトライ

い、意外と考えないといけないことってあるのね^^;

### これを使え！
じゃあどこまで自力でやんなきゃいけないかというと、まぁもちろん世の中には優秀なライブラリがあるわけで。Pythonには超優秀なScrapyというすごいやつがあります。いや、あるそうです（勉強会で知りました）。

[Scrapy \| A Fast and Powerful Scraping and Web Crawling Framework](https://scrapy.org/)

ただ、結構学習コストはかかるとのこと。でも、ドキュメントも結構充実していて、自力でやるよりは絶対いいよね？

### デモとサンプル
* [Crawl Line Fukuoka Official Site](https://gist.github.com/yu74n/7fca4bc7d7e534c8fc06c346dcbae6a2)
* [yu74n/idol\_collector](https://github.com/yu74n/idol_collector)

実際に僕も自宅に帰ってからこのGistの方のデモを試してみましたが、クッソ簡単ですね。でも取得先によって作りが結構バラバラだから、その辺どうすればいいんだろう？という。わざわざ自前で細々書いていかないといけないのか、どこかの誰かが優秀なライブラリを書いてくれているのか、はたまたScrapyをうまく使えばいいのか、、？

## リアルタイム画風変換とその未来
業務ではなく、社内ハッカソンで作られた内容だそうです。リアルタイムの画風変換、、字面だけでクッソ難しそうという印象を受けました。

※ちなみに後半はトイレに行きたすぎて半分くらい話が入ってきませんでしたorz

### 画風変換って？
オリジナル画像 + スタイル画像 = 新しい画像。

話題性あり、デモもわかりやすい。でも静止画の事例はこれまでにもたくさんあって、二番煎じ感がある。だったらリアルタイムでやれば？ということで本テーマにされたそうです。

確かに、「コレ作りました！！」って言ったらかっちょええ。デモもかっちょええ。

### 実装までの道のり
1. 最初はGPU使わないと遅くて遅くて...
1. チェイナーを参考に実装できるんでは？いやいやそう簡単な話でもなかった
1. TensorFlowでネットワークを実装
1. C++で読み込み、NDKでAndoroid上で実行
1. ここまでやっても遅い、、いい端末でもつらい、、つらいつらいつらい
1. HTTP通信で、処理をサーバーで実装すればいいじゃないか！
1. おそい、つらみつらみつらみ。
1. RTMP + FFmpeg、配信用端末 + 受信用端末
1. ビバ！リアルタイム画風変換！

半分以上何やってるのかわからないよ。ふふっ。

## LINE Developer Meetupに参加してみて
LINE Developer Meetupには、3つの旨いが揃っています！最高！ふぅー！

* ビールがうまい
* ピザがうまい
* 寿司がうまい

ただし。以下に点には注意しましょう。僕は注意できずに2つとも犯しました。ははっ。

* 乾杯前にビールを飲み干すのはやめましょう
* ビールを飲みすぎには注意しましょう（主にトイレ要因

さぁ、機械学習やるぞ！

では良き機械学習ライフを！
