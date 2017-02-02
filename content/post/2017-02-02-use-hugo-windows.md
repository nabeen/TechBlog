+++
title = "WindowsでのHugoの導入方法"
slug = "use-hugo-windows"
tags = ["Hugo", "windows"]
categories = ["Hugo"]
date = "2017-02-02T10:19:22+09:00"
description = ""
thumbnail = ""
draft = true
author = "nabeen"
+++

Windowsユーザーの皆さん、息してますか？先日からHugoを使ってブログを書き始めたんですが、仕事で使ってるWindows機でも書きたい(え←)ということで、WindowsでHugoを使う方法を残しておきます。

Macから使う方が簡単(Homebrewで入れられるし)なんですが、Windowsで使う分にもものすごく簡単！これで仕事中もブログを書くのが捗ｒ...ｹﾞﾎｯｹﾞﾎｯ

## 大まかな手順
簡単に言うと、exeファイルを落としてきてPathを通すだけで使えます。簡単楽ちん。

1. 適当にディレクトリを掘る
1. Githubからexeファイルを入手し配置
1. 配置したフォルダにパスを通す

参考サイト:[Windows で Hugo を使う \- ureta\.net](http://ureta.net/2015/05/hugo-on-windows/)

## Hugoの最新版を入手
最新版は[Releases · spf13/hugo](https://github.com/spf13/hugo/releases)にあるので、ここからDLします。

Windows以外にもLinux向けもたくさん置いてあるので、Linuxに入れたい！って場合も同じ手順で行けそうです。でもLinuxなら`yum`とか`apt-get`とかでも入れられるのかな？(知らんけど)

## exeファイルを配置する
まぁどこでもいいんですが、参考サイトに従って`C:\Hugo\bin`配下にでも置きましょう。exeファイルは`hugo.exe`にリネームして。もしバージョンが上がったら同じ手順でGithubから落としてきて差し替えればOKですね。

## Pathを通す
*がんばれ。*

## 確認する
プロンプト(何でもいい)を起動して、パスが通ってることを確認すれば終わりです。

```
$ hugo version
Hugo Static Site Generator v0.18.1 BuildDate: 2016-12-30T10:03:28+09:00
```

簡単でしたね。

それではWindowsでも良きHugoライフを！
