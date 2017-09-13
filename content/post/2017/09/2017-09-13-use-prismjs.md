+++
title = "Prismでサクッとシンタックスハイライトの導入"
slug = "use-prismjs"
description = ""
date = "2017-09-13T20:08:21+09:00"
categories = ['Hugo']
tags = ['Prism', 'SyntaxHighlight']
thumbnail = ""
author = "nabeen"
+++

ちょっとエンジニアリングに対してやる気が出てきたので、ブログもちゃんと書いていこうと思います。

んでいざ書こうと思ったら、このブログ、シンタックスハイライト入れてなかったのね。なので、今日は手軽に導入できる[Prism](http://prismjs.com/)を使います。CDNで使えるやつとかもあるみたいだけど、まぁこれくらいならローカルで持っててもいいかなーと思う。

多分もっとナウい方法があると思うんで、フロントエンドでバリバリなエンジニアは真似しちゃダメよ・ｖ・

## What's Prism
[Prism](http://prismjs.com/)

> Prism is a lightweight, extensible syntax highlighter, built with modern web standards in mind. It’s used in thousands of websites, including some of those you visit daily.

何をいいたいかよくわからないけど、ボタンポチポチすればcssとjsが組み上がるので、それをDLしてペッと貼るだけです。

## Hogoの場合
`<head></head>`で普通に読み込むだけです。超簡単ですね。僕のテーマだと(多分どのテーマにもあると思うけど)`header.html`ってのがあるんで、そこに追加で書いてます。詳しくはソースを(ry

```html
<link rel="stylesheet" href="{{ .Site.BaseURL }}css/prism.css" type="text/css" media="all" />
<script type="text/javascript" src="{{ .Site.BaseURL }}js/prism.js"></script>
```

サクッと導入できていいですね。プラグイン的なのも好きなのだけ選んで入れれるので、そのへんも好感持てます。

## Highlightサンプル
PythonのHighlightはこんな感じ。以下は追加プラグインを使って、`{.line-numbers}`でクラスを付けてあげた例です。

ちゃんと行番号も表示されてますね。

```python{.line-numbers}
import numpy as np

# see: http://prismjs.com/
print("This style use Prism.js")
```

これでコードをブログにバンバン載せられる準備ができました。ま、ちょっと長めのはGistとかにすると思いますが...
