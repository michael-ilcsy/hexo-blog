---
title: Gitで会社用アカウントと個人用アカウントを使い分ける
date: 2019-04-03 11:34:24
tags:
- Git
categories: 技術
---

**目次**
<!-- toc -->

## はじめに
gitの会社用と個人用アカウントがあり、間違えて違うアカウントを使ってコミットしてしまいあわててやり直したことが何回かあったので、自動で使い分けするようにしてみた。

## やり方
まずベースとなる`.gitconfig`の確認

```sh ~/.gitconfig
省略

[user]
	name = username
	email = hoge@fuga
```

となっているはずである。

この設定を上書きする用の`.gitconfig-private`を以下のように作成する。

```sh ~/.gitconfig-private
[user]
	name = private_username
	email = private@foo
```

そして`.gitconfig`に以下のように追記すると完成！
```sh ~/.gitconfig
省略

[includeIf "gitdir:/個人開発用のディレクトリ"]
	path = ~/.gitconfig-private
```

## 説明
何をしているのかというと、このフォルダ配下ならこの`.gitconfig`を使ってねと設定している。
この場合だと`"/個人開発用のディレクトリ"`配下なら`~/.gitconfig-private`が適用される。
あとは、個人用アカウント専用のディレクトリを作成し、そのパスを記述すれば自動で振り分けられる。


## 参考
[gitconfigで会社用アカウントと個人用アカウントを楽に使い分けする](https://qiita.com/SugarShootingStar/items/64f239f89d25a3b9f520)