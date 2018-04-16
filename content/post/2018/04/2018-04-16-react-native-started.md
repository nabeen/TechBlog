+++
title = "React Native starter different"
slug = "react-native-started"
description = ""
date = "2018-04-16T14:18:37+09:00"
categories = ['ReactNative']
tags = ['ReactNative']
thumbnail = ""
author = "nabeen"
+++

`ReactNative`を始めるにあたって、雛形を作成する手段がいくつかあります。

* `create-react-native-app`（公式サイト掲載）
* `react-native init`（公式サイト掲載）
* `exp init`（非公式）

実際に構築して、それぞれにどういう違いがあるのか調査してみました。

なお、今回の検証で利用したコードは以下のリポジトリに置いていますので、ご自由にご利用下さい。

[ReactNativeStarter](https://gitlab.com/nabeen-reference/ReactNativeStarter)

また、本記事作成にあたっては、それぞれの公式サイトを参考にしました。

* [Getting Started · React Native](https://facebook.github.io/react-native/docs/getting-started.html)
* [Installation \- Expo Documentation](https://docs.expo.io/versions/v26.0.0/introduction/installation)

## create-react-native-app

```bash
# install
$ npm install -g create-react-native-app
$ create-react-native-app RNAppWithCreateReactNativeApp

# create-react-native-app version
$ create-react-native-app --version
create-react-native-app version: 1.0.0

# structure
$ tree RNAppWithCreateReactNativeApp/ -L 1
RNAppWithCreateReactNativeApp/
├── App.js
├── App.test.js
├── README.md
├── app.json
├── node_modules
├── package.json
└── yarn.lock
```

> Install the Expo client app on your iOS or Android phone and connect to the same wireless network as your computer. Using the Expo app, scan the QR code from your terminal to open your project.

フォルダ構成、ドキュメントを見る感じ、実質`expo`を利用した開発を行う場合の雛形になる感じですね。`expo`は以前触ったことがあるんですが、**ネイティブコードは全く書かない**場合には`expo`の方がシンプルで良い印象。

個人開発であればおそらくネイティブコードは書かないように設計/実装していくと思うので、こちらの方が良さそう。

ただ実務案件ベースで考えると、要件によってはネイティブコードも書かないといけない場面に直面しそうな気がしていて、それを考えると`expo`ベースじゃない方がいいかな、という判断。

## react-native init

```bash
# install
$ npm install -g react-native-cli
$ react-native init RNAppWithReactNativeInit

# react-native version
$ react-native --version
react-native-cli: 2.0.1

# structure
$ tree RNAppWithReactNativeInit/ -L 1
RNAppWithReactNativeInit/
├── App.js
├── android
├── app.json
├── index.js
├── ios
├── node_modules
├── package.json
└── yarn.lock
```

これが王道の`ReactNative`の作り方ですね。iOS独自の、Android独自の、とかがある場合には、これを使いことになるんじゃないかと。

今はある程度`ReactNative`側で対応されてそうなので、そんなに独自処理を書くって部分は無いかも？このへんは実際に書いていかないとわかんないなぁ。

## exp init

```bash
# install
$ npm install exp --global
$ exp init RNAppWithExpo

# exp version
$ exp --version
52.0.3

# structure
$ tree RNAppWithExpo/ -L 1
RNAppWithExpo/
├── App.js
├── app.json
├── assets
├── node_modules
└── package.json
```

こちらはフルフルで`expo`に頼り切った開発をする際に使う感じになるかと思います。`expo`を触った所感は上記の通り。

## どれを使うのがベターか？

実務ベースで考えて、`react-native init`が個人的にはオススメ。

（未検証だけど）`react-native init`で作成しても`expo`での配布はできるだろうし、**とりあえずやってみる**という状況下であれば、`react-native init`で進めた方が無難かと。テストもデフォルトで設定されてるし。

もしこの辺の知見のある方いらっしゃればコメントください:D
