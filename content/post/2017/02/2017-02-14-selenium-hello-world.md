+++
draft = false
thumbnail = ""
categories = ["Python", "Selenium"]
slug = "selenium-hello-world"
date = "2017-02-15T00:55:35+09:00"
description = ""
title = "Selenium × PythonでWEBのGUIテストを自動化する為の第一歩"
author = "nabeen"
tags = ["Python", "Selenium", "pip", "OSX"]

+++

最近業務でシェルばっかり書いてて飽きてきたので、なんか別の言語を書きたい欲求が高まり、Seleniumに目をつけました。なぜSeleniumかというと、業務で使える可能性があってPythonで書けるっていう、まぁ超エンジニア的発想です。（最近の機械学習がPython一択だから、業務時間中でもPython書きたいワガママ）

もし本当にSelenium導入することになったら、、その時考えましょう。技術的負債にならないように。

## Seleniumとは
[Selenium \- Web Browser Automation](http://www.seleniumhq.org/)

簡潔にいうと、コードからブラウザを操作できる便利ツールっていう認識でいい。公式TOPには以下のように記載されています。

> Selenium automates browsers. That's it! What you do with that power is entirely up to you. Primarily, it is for automating web applications for testing purposes, but is certainly not limited to just that. Boring web-based administration tasks can (and should!) also be automated as well.

> Selenium has the support of some of the largest browser vendors who have taken (or are taking) steps to make Selenium a native part of their browser. It is also the core technology in countless other browser automation tools, APIs and frameworks.

以下訳

> Seleniumはブラウザを自動化します。それでおしまい！その力でやることは、あなた次第です。主に、テスト目的でWebアプリケーションを自動化するためのものですが、それだけではありません。退屈なWebベースの管理作業も自動化することができます。

> Seleniumは、Seleniumをブラウザのネイティブにするための手順をとっている（または行っている）最大のブラウザベンダーのサポートを受けています。無数の他のブラウザ自動化ツール、API、およびフレームワークの中核技術でもあります。

使い方は無限大、ブラウザゲームのbotで使ってもいい（）、会員制サイトのスクレイピングにつかってもいい（）、「僕のように」WEBアプリのUIテストに使ってもいい。良い子のみんなは真似しちゃダメよ。

## Selenium対応言語
* C#: NUnit
* Haskell
* Java: JUnit, TestNG
* JavaScript: WebdriverJS, WebdriverIO, NightwatchJS
* Objective-C
* Perl
* PHP: Behat + Mink
* Python: unittest, pyunit, py.test, robot framework
* R
* Ruby: RSpec, Test::Unit

参考：[Platforms Supported by Selenium](http://www.seleniumhq.org/about/platforms.jsp#programming-languages)

かなりの言語が対応してる様子。思ってたより全然多かったわ。。なんか甘く見ててすみません。。PHPもあるんですか、そうですか。

社内的なことを考慮すればPHP実装で進めるのがいいんだろうけど（メインプロジェクトがPHPなので）、別にBehatのノウハウが社内にあるわけでもないしなぁ。。。**僕はPython書きたいからPythonで始めますよ。**

ガチンコで業務導入するんなら、そん時考えればいいさ。

## Seleniumなんとかってのがたくさんある件
なんかSeleniumでググると、Seleniumなんとかってのが結構ヒットするんですよ。ハジメテダカラゼンゼンワカラナイ。え、あれもこれも必要なの？どうなの？

[Introduction — Selenium Documentation](http://www.seleniumhq.org/docs/01_introducing_selenium.jsp#selenium-s-tool-suite)

* Selenium 2
    * コイツが本体、最新版
* Selenium 1
    * 旧型、要らない子
* Selenium IDE
    * ポチポチしたのを覚えてscript吐いてくれる偉い子。使わない子。
* Selenium-Grid
    * 並列処理したい時に使えばいいっぽい。とりあえずは要らない子。

### SeleniumBase
[seleniumbase/SeleniumBase: SeleniumBase Automation Platform](https://github.com/seleniumbase/SeleniumBase)

別プロジェクトらしきコイツはなんだろう？なんか本家とは全然関係ないっぽいなぁ、、、。大人しく本家使っておけばいいのかな。とりあえずこのBaseってのは様子見で。

## 環境構築(Docker編)
ローカルを汚したくない場合は、公式からDockerが提供されているようなので、これを使いましょう。っても基本はPythonさえ動けばいいと思うんだけど。今回はとりあえず試してみるって感じなので、使いません。そもそもDocker、わかりません、、勉強します。。

[SeleniumHQ/docker\-selenium: Docker images for Selenium Standalone Server](https://github.com/SeleniumHQ/docker-selenium)

## 環境構築
今回はローカル上に環境を構築していきます。といっても必要なのは以下の3つですが。

* `pyenv`で`python`
* `pip`で`selenium`
* `brew`で`chromedriver`

```bash
$ pyenv install 3.6.0
$ pip install selenium
$ brew install chromedriver
```

※`chromedriver`はFirefoxしかテストしないなら不要です。僕は常にChromeなので当然のごとく入れています。

ちょっとうまくいかないなーって時は以下を参考にすれば多分幸せになれると思う。多分ね。後は自分でググって。

[Mac環境へのPython3系インストール \- Qiita](http://qiita.com/spyc/items/73d1295f8b3dde3b49ca)

[MacでPython 3\.5\.0インストールに失敗したら \- Qiita](http://qiita.com/maosanhioro/items/bf93540515d4ea75b222)

ちなみに執筆時点のPython、pipの最新版は以下。

```bash
$ python --version
Python 3.6.0
$ pip --version
pip 9.0.1 from /Users/nabeen/.pyenv/versions/3.6.0/lib/python3.6/site-packages (python 3.6)
```

参考：[Selenium with Python — Selenium Python Bindings 2 documentation](http://selenium-python.readthedocs.io/)

## PythonでSeleniumを使う
さぁ、あとはコード書くだけです！

あれ？最初に言ったSeleniumなんとかは？そう、要らないんです／(^o^)＼

pythonでやるんだったら、`pip`で`selenium`入れちゃえば、もうそれだけでseleniumが使えちゃう。わーい！すごーい！

で、初めて書いたPythonコードがこちら。元ネタは[PythonとSeleniumでネットバンキングをスクレイピングする · >> work\.log](http://blog.mursts.jp/entry/2015/09/25/scrape-netbanking-by-python-and-selenium/)を参考にさせていただきました！感謝。

```python
import unittest
import time
from selenium import webdriver

class GoogleTestCase(unittest.TestCase):

    def setUp(self):
        self.browser = webdriver.Chrome()
        self.addCleanup(self.browser.quit)

    def testPageTitle(self):
        try:
            SEARCH_WORD = 'python'
            self.browser.get('http://www.google.com')
            self.assertIn('Google', self.browser.title)
        finally:
            self.browser.quit()

    def testSearchTitle(self):
        try:
            SEARCH_WORD = 'python'
            self.browser.get('http://www.google.com')
            time.sleep(3)
            search_input = self.browser.find_element_by_name('q')
            search_input.send_keys(SEARCH_WORD)
            search_input.submit()
            time.sleep(3)
            self.assertIn(SEARCH_WORD + ' - Google 検索', self.browser.title)
        finally:
            self.browser.quit()

if __name__ == '__main__':
    unittest.main(verbosity=2)
```

## おわりに
とりあえず動いたけど、Python初見だから書き方が全然わからん／(^o^)＼

テスティングライブラリのunittestってのを使ってるようだけど、他にもあるのかな、、Pythonのテスティングライブラリ。PHPならほぼPHPUnit一択なんだけど；；

まぁ次回以降はコード書きながらPythonそのものを学びつつSeleniumのメソッドを調べていく感じかな。出来ないこととかあったら先に知りたい感。

それではよきSeleniumライフを！
