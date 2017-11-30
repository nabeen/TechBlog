+++
title = "vagrant upしたらSSHのコネクション周りで怒られたので解決する"
slug = "vagrant-ssh-connection"
description = ""
date = "2017-11-30T17:19:59+09:00"
categories = ['vagrant']
tags = ['vagrant','ssh']
thumbnail = ""
draft = false
author = "nabeen"
+++

まだvagrant使ってるの？とかは言わないでください。

今から新規で作るならdockerですが、その昔はまだdockerとも全く友達じゃなかったので。今は顔見知りくらいにはなりましたが:D

ともあれ、vagrantを立ち上げ直した時に発生したエラーと、解決方法をメモしておきます。

## 発生したエラー
両方とも、`vagrant up`した時に発生したエラーです。

```bash
An error occurred in the underlying SSH library that Vagrant uses.
The error message is shown below. In many cases, errors from this
library are caused by ssh-agent issues. Try disabling your SSH
agent or removing some keys and try again.

If the problem persists, please report a bug to the net-ssh project.

timeout during server version negotiating
PC-4037:vagrant-hubot yukimura$ vagrant ssh
VM must be running to open SSH connection. Run `vagrant up`
to start the virtual machine.
```

とか、

```bash
Timed out while waiting for the machine to boot. This means that
Vagrant was unable to communicate with the guest machine within
the configured ("config.vm.boot_timeout" value) time period.

If you look above, you should be able to see the error(s) that
Vagrant had when attempting to connect to the machine. These errors
are usually good hints as to what may be wrong.

If you're using a custom box, make sure that networking is properly
working and you're able to connect to the machine. It is a common
problem that networking isn't setup properly in these boxes.
Verify that authentication configurations are also setup properly,
as well.

If the box appears to be booting properly, you may want to increase
the timeout ("config.vm.boot_timeout") value.
```

とか。

共通して言えることは、sshのコネクション周りでエラーを吐いて接続できない状態になっているということ。

ググると、`ssh-agent`が悪さしてるだの、一回`destroy`すれば直るだの、`Vagrantfile`に追記すればいいだの言われますが、僕のケースでは一向に改善せず。

参考：

* [OSX で vagrant up したときのエラー \- Qiita](https://qiita.com/kazusanto/items/8ad89fb3fe8ae1bd5d81)
* [An error occurred in the underlying SSH library that Vagrant uses\. · Issue \#7965 · hashicorp/vagrant](https://github.com/hashicorp/vagrant/issues/7965)
* [VCCW構築時にハマる（vagrant up で失敗） \| rinteq\.com](http://rinteq.com/?p=2627)

試しに別のマシンで試してみたところ走り出したので、`Vagrantfile`そのものが悪いわけではなさそうでした。

## 解決方法
僕のケースでは、`.vagrant`をぶち消してやれば改善しました！なんか変なデータが残ってたのかな？

```bash
$ rm -rf .vagrant
```

リンク先では`.vagrant.d`も消してたみたいですが、そこまでは消さなくても大丈夫だったようです。

参考：

* [Homestead vagrant up error](https://laracasts.com/discuss/channels/servers/homestead-vagrant-up-error)

ご参考まで。
