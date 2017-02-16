+++
tags = ["Selenium", "Python", "FiremobileSimulator"]
title = "SeleniumでFirefoxのFiremobileSimulatorを利用する"
draft = true
description = ""
thumbnail = ""
slug = "selenium-firemobile-simulator"
categories = ["Selenium", "Python"]
date = "2017-02-17T01:45:54+09:00"
author = "nabeen"

+++

Selenium、結構簡単で楽しいですね。Seleniumを使うこと自体のオーバーヘッドはほとんどなくって、Pythonで書いているので、Pythonそのものの書き方がちょっとネックになってる感じです。ま、Python書いたこと無いんでね。

## FiremobileSimulatorを使いたい
僕が今担当しているプロジェクトは結構レガシーなサービスなので、ガラケー向けにも展開しています。個人的にはガラケーはこの世から抹消されればいいのにと思ってるんですが；；

とはいうものの、捨てるわけにはいかないので対応するわけですが、PCから検証する際に役に立つのが、皆さんおなじみ、FiremobileSimulatorです。

それを、Seleniumから使いたい。さぁ、こんなこと出来るんでしょうか。もちろんできます。しかも全然手間じゃない。

## やり方
以下の手法でFiremobileSimulator起動状態でSeleniumで立ち上げることが出来ます。

1. Selenium用のプロファイルを作成する
1. FiremobileSimulatorを起動した状態のプロファイルを上記で作成したプロファイルにコピーする
1. Selenium用のプロファイルのファイルを読み込み、webdriverを作成する際に引数として渡す

詳細は以下のサイトが参考になりました。感謝。

[まこちの技術情報覚え書き　SeleniumとFireMobileSimulatorの連携](http://wavetalker.blog134.fc2.com/blog-entry-76.html)

[seleniumでガラケー環境を構築したい人必見！mac上のseleniumでFireMobileSimulatorを動かす方法はこれだ。 \- Qiita](http://qiita.com/hayakawatomoaki/items/6be743ba98cd8ad41248)

## サンプルコード
コードは汚いですが、以下のような感じで使えます。

```python
import unittest
import time
from selenium import webdriver
from selenium.webdriver import FirefoxProfile

# SeleniumでFiremobileSimulatorを使ってみるサンプル
class GoogleTestCase(unittest.TestCase):

    def setUp(self):
        profile = FirefoxProfile(self.getProfileData());
        self.browser = webdriver.Firefox(profile)
        self.addCleanup(self.browser.quit)

    def getProfileData(self):
        # ファイルから読み込み、1行目にプロファイルのフルパスが書いてある想定
        f = open('.FireMobileSimulatorSettings')
        lines = f.read()
        f.close()
        lineArray = lines.split('\n')
        for line in lineArray:
            return line
        return

    def testPageOpen(self):
        self.browser.get('http://google.com')
        time.sleep(3)

if __name__ == '__main__':
    unittest.main()
```

`.FireMobileSimulatorSettings`の1行目にプロファイルまでのファイルパスが書かれている想定です。例えばwindowsならこんな感じ。

```
C:\Users\nabeen\AppData\Roaming\Mozilla\Firefox\Profiles\hogehoge.Selenium
```

## おわりに
なんかたいして苦労することもなくサクサク書ける感じがいいですね。あとはPythonを使いこなせれば難なく実案件向けのコードを書いていけそうな予感がしています。ただ、導入するか自体は、メンバーと相談なんですけどね。運用改善って意味ではマイネットさんの[【速報2】マイネット、AIによる自動運転を導入…月商1000万円台のタイトルで検証開始 \| Social Game Info](http://gamebiz.jp/?p=178479)ってのが非常に気になるところ。

それでは良きSeleniumライフを！
