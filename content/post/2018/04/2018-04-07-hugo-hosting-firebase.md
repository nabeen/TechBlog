+++
title = "Deploy Hugo site on Firebase with wercker"
slug = "hugo-hosting-firebase"
description = ""
date = "2018-04-07T01:25:55+09:00"
categories = ['Firebase', 'Hugo']
tags = ['Firebase', 'Hugo', 'wercker']
thumbnail = ""
draft = false
author = "nabeen"
+++

本ブログはこれまでGithubPagesにホストしており、ドメインはgithub.ioのサブドメインだったんですが、今回もろもろ整理したので、そ備忘録です。

## 変更前

* ホスト先：GithubPages
* ドメイン：nabeen.github.io

## 変更後

* ホスト先：Firebase
* ドメイン：tech.nabeen.be

## Firebaseに変更した経緯

github.ioのドメインもそれなりに気に入ってはいたんですが、かねてより独自ドメインにしたいなぁとは思っていました。思ってはいたんですが、GithubPagesでそれをやるにはなかなか面倒で、重い腰が上がらなかった。

そんな中で、別途作ったポートフォリオサイトをFirebaseにホストしてみたんですが、SSL対応を勝手にやってくれていい感じだったので載せ替えました。

## wercker.ymlの設定内容

こちらが変更前の状態。ビルドして、GithubにPushするような設定。

```yml
box: debian
build:
  steps:
    - arjen/hugo-build@1.21.1:
      version: "0.36"
      flags: --buildDrafts=false
      theme: even
deploy:
  steps:
    - install-packages:
        packages: git ssh-client
    - leipert/git-push:
        gh_oauth: $GIT_TOKEN
        basedir: public
        repo: nabeen/nabeen.github.io
        branch: master
```

そしてこちらが変更後の状態。ビルドして、Firebaseにデプロイする設定。`$FIREBASE_PROJECT`、`$FIREBASE_TOKEN`はwercker側で環境変数として定義しています。さすがに公開できないですからね...。

```yml
box: node
build:
  steps:
    - script:
      name: install wget
      code: |
        apt-get update
        apt-get -y install wget
    - script:
      name: wget hugo
      code: |
        wget https://github.com/gohugoio/hugo/releases/download/v0.38.1/hugo_0.38.1_Linux-64bit.deb && dpkg -i hugo*.deb
    - script:
      name: build hugo site
      code: |
        hugo -d public
deploy:
  steps:
    - script:
      name: install firebase-tools
      code: |
        npm install -g firebase-tools
    - script:
      name: deploy firebase
      code: |
        firebase deploy --project "$FIREBASE_PROJECT" --token "$FIREBASE_TOKEN" --only hosting
```

変更後は、見た目ちょっと美しくはないですが、`script`とかでコマンドを書いているので、何してるかは一目瞭然でわかるのが良い。

あとはGithubにPushするだけでFirebaseへのデプロイまで自動でやってくれます。楽ちんでいいですね。

実はついでにテーマも[hugo\-theme\-jane](https://github.com/xianmin/hugo-theme-jane)に変えたので、ちょこちょこ手直し中。

**Firebaseはいいぞ。**
