+++
title = "[開発日誌]day1.Create First React Native Apps"
slug = "react-native-starter"
description = ""
date = "2018-05-26T02:30:02+09:00"
categories = ['React Native']
tags = ['React Native']
thumbnail = ""
author = "nabeen"
+++

これまでサーバーサイド（主に`PHP`）しか実務で使ったことがなく、そろそろAndroid/iOSくらいは組めるようになりたいので、個人プロジェクトとして進めていくことにしました。

とは言えiOSアプリを個人でバリバリ作っていく機運は全く無く（維持費が高いので）、Androidメインの予定です。なので`Kotlin`でアプリを作りつつ、必要であればAPIも`Kotlin`で実装するつもりでした。

ただ仮に実務でネイティブをやるとなると、自社のリソース的にはクロスプラットフォームな技術選定をするはず。なので業務でも活かせるように、今回は`React Native`でクロスプラットフォームなプロダクト開発をしていきます。

## 筆者のスキル

前述した通り、僕の現在のスキルレベルはこんな感じです。まさにゼロからのスタート。

* フロントエンド苦手
* React経験無し
* ネイティブ（ほぼ）経験無し

それではやっていきます。

## 本日行うこと

本日は、サクサク実装する前準備をしていきます。

* React Nativeのプロジェクトを作成
* ESLint、flowの設定

## プロジェクトの作成

必要なパッケージは事前に入れてある想定です。必要なパッケージは公式サイトを参考にしてください。

参考記事：[Getting Started · React Native](https://facebook.github.io/react-native/docs/getting-started.html)

```bash
# react-nativeのバージョン
$ react-native -v
react-native-cli: 2.0.1
react-native: 0.55.4
```

```bash
# react-nativeで雛形の作成
$ react-native init project_name
```

## 立ち上げ

好き方で立ち上げてください。

### iOSの場合

```bash
$ react-native run-ios
# 指定したエミュレータで起動する
$ react-native run-ios --simulator="iPhone X"
```

### Androidの場合

```bash
$ react-native run-android
```

## ESLint導入

ルールセットについてはお好みで選択してください。

```bash
# グルーバルESLintを導入
$ npm install -g eslint
# --devで使用するルールセットを導入
$ yarn add --dev eslint-config-rallycoding
```

`.eslintrc`の設定は以下のように設定しました。

```json
{
  "extends": "eslint-config-rallycoding",
}
```

とりあえず`extends`のみ設定していますが、その他の設定項目については公式サイトを参照してください。ただし、基本は`extends`しているルールセットに則るので、以降大量に追加することはありません。

参考記事：[ESLint \- Pluggable JavaScript linter](https://eslint.org/)

## （EditorConfigの導入）

お好みでどうぞ。

```ini
# EditorConfig helps developers define and maintain consistent
# coding styles between different editors and IDEs
# editorconfig.org

root = true

[*]
# Change these settings to your own preference
indent_style = space
indent_size = 2

# We recommend you to keep these unchanged
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

# Use 4 spaces for the Python files
[*.py]
indent_size = 4
max_line_length = 80

# Use 4 spaces for the PHP files
[*.php]
indent_size = 4

# The JSON files contain newlines inconsistently
[*.json]
insert_final_newline = ignore

# Minified JavaScript files shouldn't be changed
[**.min.js]
indent_style = ignore
insert_final_newline = ignore

# Makefiles always use tabs for indentation
[Makefile]
indent_style = tab

# Batch files use tabs for indentation
[*.bat]
indent_style = tab

[*.md]
trim_trailing_whitespace = false
```

## flowの設定

`flow`のバージョンは、`.flowconfig`に記述してあるものと一致していないとエラーになるので、バージョン指定で導入してください。

参考記事：[Getting Started with React Native and Flow – React Native Training – Medium](https://medium.com/react-native-training/getting-started-with-react-native-and-flow-d40f55746809)

```bash
$ yarn add flow-bin@0.67.1 --dev
```

また、`flow`の記述で型指定しますが、普通にバリデーションしてしまうと警告が出るので、VS Codeの設定でバリデーションを切っておきます。

```json
{
    "javascript.validate.enable": false
}
```

参考記事：[\[Flow\] type can be used by only '\.ts' files? · Issue \#5214 · Microsoft/vscode](https://github.com/Microsoft/vscode/issues/5214)

自動実行をするのであれば、エディタ拡張などで対応してください。VS Codeならこちらのプラグインを導入すれば大丈夫です。

参考記事：[flowtype/flow\-for\-vscode: Flow for Visual Studio Code](https://github.com/flowtype/flow-for-vscode)

## まとめ

ここまでで次回以降にサクサク実装していく前準備ができました。`ESLint`とか`flow`は自分で設定しないといけないのが、多少面倒だなと思いました。どうせだからデフォルトで組み込んでくれればいいのに...

それでは次回以降、実装していきます。
