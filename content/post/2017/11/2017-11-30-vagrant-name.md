+++
title = "vagrant up時にnameを指定できるって知ってました？"
slug = "vagrant-name"
description = ""
date = "2017-11-30T17:24:54+09:00"
categories = ['vagrant']
tags = ['vagrant']
thumbnail = ""
draft = false
author = "nabeen"
+++

今日初めて知りました。

へーしゃではChatWorkとHubotを連携させてChatOpsをしているんですが、そのHubotを立てるのにVagrantを使っています。

で、`vagrant up`する時に開発用と本番用で走らせるスクリプトを変えているので引数を渡して立ち上げているんですが、そこに潜んでいた罠の話。

## VMの立ち上げ方
普通はこうやって立ち上げると思うんですが、

```bash
$ vagrant up
```

へーしゃの場合、こんな感じで立ち上げています。

```bash
# for develop
$ vagrant up dev
# for production
$ vagrant up prod
```

で`Vagrantfile`（といっても中身はRubyなので）内で`ARGV`で受け取って引数によって処理を振り分けています。

本番用は起動処理も実行させたいので`forever`でデーモン化して、、とか、まぁそんな感じの処理です。ちょっとイレギュラーですが。

## 作ったはずのVMが作られてない？
ところが、です。

上記で作成したVMに対して`ssh`しようとしてもできない。

```bash
$ vagrant ssh
VM must be created before running this command. Run `vagrant up` first.
```

いや、ちゃんと`vagrant up`はしてるんですよ。多少の`warning`はご愛嬌として、正常に起動してるんです。

だがしかし。`status`を見ても作られてないことになってます。

```bash
$ vagrant status
Current machine states:

default                   not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
```

これはどういうことなんだろうか…

## ヘルプを見てみる
困った時のヘルプを見てみます。すると。

```bash
$ vagrant up --help
Usage: vagrant up [options] [name|id]

Options:

        --[no-]provision             Enable or disable provisioning
        --provision-with x,y,z       Enable only certain provisioners, by type or by name.
        --[no-]destroy-on-error      Destroy machine if any fatal error happens (default to true)
        --[no-]parallel              Enable or disable parallelism if provider supports it
        --provider PROVIDER          Back the machine with a specific provider
        --[no-]install-provider      If possible, install the provider if it isn't installed
    -h, --help                       Print this help
```

なんということでしょう。`Usage: vagrant up [options] [name|id]`という文字列が見えるではありませんか。

つまり、単なる引数として渡していたつもりのものが、`[name|id]`として認識されてるわけですね。なるほど。

## 改めてstatusを確認してみる
つまり、`[name|id]`をつけてVMを作ったんだから、`ssh`する時も同様に`[name|id]`をつけろってことなんですね。

試しに引数をつけて見てみると、きちんと起動していることがわかります。もちろん`ssh`する時は`vagrant ssh prod`ですね。

```bash
$ vagrant status prod
Current machine states:

prod                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```

## おわりに
僕も`Vagrant`歴はまぁまぁそれなりに長いんですが、初めて知るものがあろうとは…（`Vagrantfile`は結構知らないの多いけど）。

`vagrant up`に引数渡して処理するのなんてかなりのイレギュラーケースだと思いますが、下手すればどハマりするので気をつけてください（僕は30分くらいはハマりました）。
