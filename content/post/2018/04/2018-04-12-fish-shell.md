+++
title = "Change shell from zsh to fish shell"
slug = "fish-shell"
description = ""
date = "2018-04-12T22:31:33+09:00"
categories = []
tags = []
thumbnail = ""
draft = true
author = "nabeen"
+++

これまでずっと迷うことなく`zsh` + `oh-my-zsh`を使っていたんですが、ひょんなことから乗り換えました。

そう、fish shellに。

**fish shellはいいぞ。**

## 導入のきっかけ

**環境がぶっ壊れたからそのついで**です。なんかネガティブな理由ですいません。

会社で使ってるサブPC(OS X)のバージョンを上げたんですが、その時に見事色々ぶっ壊れました。まぁよくあることだし、大した設定をしていたわけでもないので、えいやで上げたんですが、まあ見事に壊れたよね。

ちまちま修復していってももちろんいいんですが、なんかめんどくせえなと思ってしまって。

んで、せっかくだから乗り換えてみようかなと。

ちょっと前にfish shellってものを見かけたので、それを使ってみることにしました。

## 変更前後

変更前の組み合わせがこれで、

* `zsh` + `oh-my-zsh`

変更後の組み合わせがこちら。

* `fish` + `fisherman`

変更前もそこまでカスタマイズしていたわけでもないので、とりあえずデフォルトの機能でも問題はなさそう。

## 導入方法

こちらをまんまパクりました。さすがDevelopers.IOです。

[fish shell を使いたい人生だった ｜ Developers\.IO](https://dev.classmethod.jp/etc/fish-shell-life/)

```bash
# fishのインストール
$ brew install fish
$ fish -v
fish, version 2.7.1

# ログインシェルの変更
$ sudo vi /etc/shells #/usr/local/bin/fish
$ chsh -s /usr/local/bin/fish

# fishermanの取得
$ curl -Lo ~/.config/fish/functions/fisher.fish --create-dirs git.io/fisher
$ fisher -v
fisherman version 2.13.2 ~/.config/fish/functions/fisher.fish

# テーマの変更/フォントのインストール
$ fisher install omf/theme-bobthefish
$ git clone git@github.com:powerline/fonts.git
$ sh fonts/install.sh
```

あとプラグインをお好きに。

## 所感

とりあえず、起動がめっちゃ速くなりました。

やっぱり`oh-my-zsh`は重量級だったんだなぁと実感。テーマもPowerline系のフォントのやつ使ってて、branchがいい感じ見えてなかなかよい。

挙動的にはやっぱり`oh-my-zsh`と違う部分が結構ありますが、このへんは慣れながら使いこなしていけばいいかな。

以上、簡単ですが、`fish` + `fisherman`のご紹介でした。
