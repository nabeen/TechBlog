+++
draft = false
tags = ["macOS", "ssh", "Keychain", "Password"]
slug = "mac-ssh-password"
thumbnail = ""
categories = ["macOS"]
title = "macOS Sierraでsshする時に秘密鍵のパスワードを毎回求められる場合の対処法"
date = "2017-02-16T03:07:09+09:00"
description = ""
author = "nabeen"

+++

会社のMacではそんなことないんだけど、自前のMacbookでsshすると、なぜか毎回パスワードを求められます。なぜかKeychainに保存されないんです。今まではssh-agentとか使って登録してたんだけど、結局再起動したらやり直しだし、面倒くさい！ってことで、原因を調べてみました。

さすがにpull、pushの度にパスフレーズ入力するのがつらくなってきた；；

## 予想
最初は以下の予想をしていました。

* 公開鍵/秘密鍵の権限が間違っている
* `.ssh`ディレクトリの権限が間違っている
* そもそも公開鍵/秘密鍵がペアになってない
* なんかのキャッシュが邪魔している

ま、結果、全部違ったんですけど；；

ハハ、僕の力量なんてこんなもんです。しゃーないしゃーない。

## 原因
どうやらmacOS Sierraで使われているsshのバージョンが原因の模様。

```bash
$ ssh -V
OpenSSH_7.3p1, LibreSSL 2.4.1
```

参考：[macOS Sierra の SSH で、秘密鍵のパスフレーズが Keychain 保存されない問題の解決方法 \- HAM MEDIA MEMO](https://h2ham.net/macos-sierra-use-keychain)

社用MacはSierraにしてないから大丈夫なわけだ。なるほど合点がいった。

## 解決法
`~/.ssh/config`に以下の設定を書く。これだけ！

```
AddKeysToAgent yes
UseKeychain yes
```

これを書くことでいつものようにsshがパスレスになった。快適快適（というかこれが普通。pull，pushも当然パスレス！ヒャッハー！

それでは良きsshライフを！
