+++
title = "Raspberry Piにsshする"
slug = "raspberry-ssh"
description = ""
date = "2017-08-08T20:22:13+09:00"
categories = ["Raspberry Pi"]
tags = ["Raspberry Pi", "ssh"]
thumbnail = ""
author = "nabeen"
+++

少し前の話になりますが、Raspberry Pi Zero Wを入手したので、ssh接続の設定までしていきます。スペックはちょっとしょぼいけど、ケースキットで3000円程度と激安！オススメです。

※ただしまだGPIOピンをゲットしていないので、IoTはもとより、Lチカすらできていないのは内緒の話。

## 前提条件
Wi-Fiの設定やら、その他の基本的な設定は、GUIで設定しているものとします。

## この記事を読んで出来るようになること
- 同一LAN内の

## ssh接続を有効化する
Raspberry Piは簡単なもので、GUIライクでsshの設定ができます。

```bash
$ sudo raspi-config
```

コマンドをッターンすれば以下の画面が立ち上がるので、`5 Interfacing Options`を選択。※画面はssh済みのmacからのスクショです、、あしからず。

[![https://gyazo.com/61c234f92d7adcfcc45ef49b2ae8cd09](https://i.gyazo.com/61c234f92d7adcfcc45ef49b2ae8cd09.png)](https://gyazo.com/61c234f92d7adcfcc45ef49b2ae8cd09)

`P2 SSH`からの

[![https://gyazo.com/4523898efd2204d43c7f0cba85dd018f](https://i.gyazo.com/4523898efd2204d43c7f0cba85dd018f.png)](https://gyazo.com/4523898efd2204d43c7f0cba85dd018f)

`はい`を選択すればOK。

[![https://gyazo.com/a610dff06ebbed1aa83853a7905bbb79](https://i.gyazo.com/a610dff06ebbed1aa83853a7905bbb79.png)](https://gyazo.com/a610dff06ebbed1aa83853a7905bbb79)

とりあえずここまでで、繋がるはず。

`ifconfig`で今のIPアドレスを見てあげて、`ssh`します。僕の場合`192.168.0.10`だったので、初期ユーザーでログインするなら以下のコマンドをッターンしてください。

```bash
$ ssh pi@192.168.0.10
pi@192.168.0.10's password: raspberry
```

後はお好みでIP固定とかすればOK。僕は外部からsshできるようにする時にでもやろうかなって思ってます。

最近全然家でコード書いてないし、やる気も全くでしたが、IoTができる楽しいオモチャも手に入れたことだし、`Python`でなんか楽しいコードでも書こうかなっていう気持ちが少し出てきた今日でした・ω・
