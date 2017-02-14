+++
draft = true
thumbnail = ""
categories = ["Python", "Selenium"]
slug = "selenium-hello-world"
date = "2017-02-14T20:08:29+09:00"
description = ""
title = "Selenium × PythonでWEBのGUIテストを自動化する為の第一歩"
author = "nabeen"
tags = ["Python", "Selenium", "pip", "OSX"]

+++

最近業務でシェルばっかり書いてて飽きてきたので、なんか別の言語を書きたい欲求が高まり、Seleniumに目をつけました。なぜSeleniumかというと、業務で使える可能性があってPythonで書けるっていう、まぁ超エンジニア的発想です。（最近の機械学習がPython一択だから、業務時間中でもPython書きたいワガママ）

もし本当にSelenium導入することになったら、、その時考えましょう。技術的負債にならないように。

## Seleniumとは
[Selenium \- Web Browser Automation](http://www.seleniumhq.org/)

簡潔にいうと、コードからブラウザを操作できる便利ツールっていう認識でいいでしょう。公式TOPには以下のように記載されています。

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

かなりの言語が対応してますね。PHPもあるんですか、そうですか。社内的なことを考慮すればPHP実装で進めるのがいいんだろうけど、別にBehatのノウハウが社内にあるわけでもないし。。。**僕はPython書きたいからPythonで始めますよ。**

ガチンコで業務導入するんなら、そん時考えればいいさ。

## Seleniumなんとかってのがたくさんある件
なんかSeleniumでググると、Seleniumなんとかってのが結構ヒットするんですよ。

[Introduction — Selenium Documentation](http://www.seleniumhq.org/docs/01_introducing_selenium.jsp#selenium-s-tool-suite)

* Selenium 2
    * コイツが本体、最新版
* Selenium 1
    * 旧型、要らない子
* Selenium IDE
    * ポチポチしたのを覚えてscript吐いてくれる偉い子。使わない子。
* Selenium-Grid
    * 並列処理したい時に使えばいいっぽい。とりあえずは要らない子。

[seleniumbase/SeleniumBase: SeleniumBase Automation Platform](https://github.com/seleniumbase/SeleniumBase)

別プロジェクトらしきコイツはなんだろう？なんか本家とは全然関係ないっぽいなぁ、、、。大人しく本家使ったほうがいいような気がしてるよ。

## 環境構築
ラッキー、公式からDockerが出てるよ。これ使えるかな？
[SeleniumHQ/docker\-selenium: Docker images for Selenium Standalone Server](https://github.com/SeleniumHQ/docker-selenium)

## PythonでSeleniumを使う
[Selenium with Python — Selenium Python Bindings 2 documentation](http://selenium-python.readthedocs.io/)

```bash
pip install selenium
```

[PythonとSeleniumでネットバンキングをスクレイピングする · >> work\.log](http://blog.mursts.jp/entry/2015/09/25/scrape-netbanking-by-python-and-selenium/)

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
