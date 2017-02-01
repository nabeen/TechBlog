+++
title = "Hugoの公式テーマであるmainroadのCSSをカスタマイズする"
slug = "custom-css-mainroad"
thumbnail = ""
tags = ["css", "Hugo"]
categories = ["css"]
date = "2017-02-02T00:02:47+09:00"
description = ""

+++

[GithubPagesにHugoで作ったサイトをホスティングする](https://nabeen.github.io/github-hugo-wercker/)でも書いたが、ひとまずこのブログでは公式テーマである[Mainroad](http://themes.gohugo.io/mainroad/)を使うことにした。ただ、このテーマに全て満足しているわけもなく、いくつかカスタマイズしたいなぁという部分があったので、今回はカスタム方法についてサクッと書いておく。

## Hugoのテーマをカスタムするには？
これはCSSだけに限った話ではないが、Hugoはthemeファイルを読みにいったあと、プロジェクト内で独自定義されている同名のファイルがあればオーバーライドして適用される。つまりどういうことかというと、テーマファイル内に`/themes/mainroad/static/css/style.css`があって、プロジェクト内に`static/css/style.css`があればオーバーライドして適用してくれるわけ。ということは、テーマ自体を触らずに独自定義部分のみ外出しできる仕組みになってるってことだ。

まぁ言ってみればWordPressの子テーマ的な運用が可能な仕組みになっていると考えて差し支えない。

## mainroadに独自定義のCSSを書く
mainroadには残念ながらデフォルトで独自用のCSSの設定がされていないので、本体をいじっていく（気になる方はプロジェクト内にコピーしてそれを変えるのもあり）。イマドキでホスピタリティ精神ありありなテーマだとこの辺りもきちんと整備されているので、ちょっと残念な部分ではある。ま、ちょっと追加するだけなんだけどね！

まずは`layouts/partials/header.html`に独自CSSを読み込む設定を書く。普通のCSSの読み込み設定。

```html
<link rel="stylesheet" href="{{ .Site.BaseURL }}css/custom.css" type="text/css" media="all" />
```

あとは`static/css/custom.css`を普通に書いていけばいい。ちなみに現時点で僕はこんな感じのCSSを追加している。

```css
/* 背景色 */
body {
	background: #FFF;
}

/* 影の取り消し */
.mr-container-outer {
	margin: auto;
	-webkit-box-shadow: none;
}

/* フッターの横幅調整 */
.mr-copyright-wrap {
	margin-left: -500%;
	margin-right: -500%;
	padding-left: 500%;
	padding-right: 500%;
}

/* ナビゲーションの横幅調整 */
.menu {
	margin-left: -500%;
	margin-right: -500%;
	padding-left: 500%;
	padding-right: 500%;
}

/* リストスタイル */
.entry-content ul li {
	padding:0px;
	margin:0px;
}

.entry-content ul li {
	list-style-type:none !important;
	list-style-image:none !important;
	margin: 5px 0px 5px 0px !important;
}

.entry-content ul li {
	position:relative;
	padding-left:20px;
}

.entry-content ul li:after, .entry-content ul li:before{
	content:'';
	display:block;
	position:absolute;
	top:4px;
	left:8px;
	height:11px;
	width:4px;
	background:#aaa;
	border-radius:10px;
	transform:rotate(45deg);
	-webkit-transform:rotate(45deg);
	-o-transform:rotate(45deg);
}
.entry-content ul li:before{
	top:8px;
	left:3px;
	height:8px;
	transform:rotate(-45deg);
	-webkit-transform:rotate(-45deg);
	-o-transform:rotate(-45deg);
}

.entry-content ol {
  counter-reset: my-counter;
  list-style: none;
  padding: 0;
}

.entry-content ol li {
  margin-bottom: 10px;
  padding-left: 30px;
  position: relative;
}
.entry-content ol li:before {
  content: counter(my-counter);
  counter-increment: my-counter;
  background-color: #e64946;
  color: #ffffff;
  display: block;
  float: left;
  line-height: 22px;
  margin-left: -30px;
  text-align: center;
  height: 22px;
  width: 22px;
  border-radius: 50%;
}

/* authorboxスタイル */
.mr-author-box-avatar, .mr-author-box-avatar img {
	border-radius: 50%
}

/* タグクラウドスタイル */
.tagcloud a {
	border-radius: 10px
}

/* codeスタイル */
.entry-content p code {
	padding: 0.2em;
	padding-top: 0.2em;
	padding-bottom: 0.2em;
	margin: 0.2em;
	font-size: 85%;
	background-color: rgba(0,0,0,0.04);
	border-radius: 3px;
}
```

これは執筆時点の最新版なので、本エントリ投稿以降に追加されたようなものに関しては、直接[nabeen/blog](https://github.com/nabeen/blog)を見に行ってもらえればいいかと。

今回はこれ普通に書いちゃったんだけど、Gulpとか使ってSCSSで書いた方がいいんじゃないかなぁと思ったりもしている。ちょうどCSSの勉強したばっかりだし。BEM！BEM！

## 今後やりたいカスタム
デザイン自体は嫌いじゃないんだけど、結構足りない部分が目立つなぁという印象。

* コメント(Disqus)追加
* GoogleAnalytics追加
* 広告枠追加
* フォント調整
* グローバルナビの手動設定

ざっとこれくらいはやりたいかな。はてなとかと違って、全部いじりたい放題なので僕のやる気さえあれば全て実現するヤツですね。最終独自ドメインでもとろうかなぁ。

それではよきHugoライフを！
