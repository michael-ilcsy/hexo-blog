---
title: Netlifyでデプロイ
date: 2019-02-27 19:08:16
categories: 技術
tags:
- Netlify
---

出来上がったHexoブログをNetlifyでデプロイしてみる。
今回Netlifyを選んだのは
* Githubとの連携できる
* ビルド時のコマンド指定などが出来る
* 軽くて速い
* 無料枠が大きい

という理由から。

**目次**
<!-- toc -->

## 事前準備
NetlifyはGithubとの連携が強力(だと思っている)ので、あらかじめGithubアカウントの作成とGithubリポジトリへのHexoブログのソースのpushを行っておく。

## Netlifyの登録とGithubとの連携
登録と連携はいろんなサイトで解説されている(記事の最後の参考リンクも詳しい)ので省略。
個人的に少しだけハマったのは、privateリポジトリなどで開発していると、その都度リポジトリにアクセスできる権限をNetlifyに与える作業をしなくてはいけない。
これに気付かず10分ほどうんうん唸っていた。

## 公開ディレクトリやビルドコマンドの登録
色々設定しなくてはいけないが、主にやっておかないといけないものだけ挙げておく。
`Site settings > Build & deploy > Build settings`の以下のものは正しく設定しないとビルドが全く通らない(当たり前)

```
//ビルドコマンドを実行するディレクトリのリポジトリルートからのパス
Base directory : /hoge

//ビルドコマンド
Build command : hexo generate

//公開するディレクトリのリポジトリルートからのパス
Publish directory : /hoge/public
```


## 参考
[HexoとNetlifyで快適なブログ環境を手に入れよう！](https://blog.engineer.adways.net/entry/2018/10/19/150000)