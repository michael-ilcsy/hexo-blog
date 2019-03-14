---
title: NodeでCheerioを使ってスクレイピング
date: 2019-03-14 12:00:22
tags:
- Node
- Cheerio
- スクレイピング
categories: 技術
---

スクレイピングをやったことが無かったが、軽く情報を取得したいということがあったので試しにNodeでスクレイピングしてみた。

**目次**
<!-- toc -->


## ライブラリの準備
今回はスクレイピングに[cheerio-httpcli](https://www.npmjs.com/package/cheerio-httpcli)を使用する。
`cheerio`はてパースしたHTMLをjQueryのように操作できるライブラリで、`cheerio-httpcli`はそれを更に使いやすくしたもの。
ということでインストールする。今回はこれ以外は使わない。(必要に応じて`lodash`等は入れてもいいかもしれない。)
```bash
yarn add cheerio-httpcli
```

## スクレイピング
### 使い方
大体 [ここ](https://blog.honjala.net/entry/2018/08/17/005719) を参考にした。

簡単な使い方だけ書いておく。

```js
const httpClient = require('cheerio-httpcli');

const main = async () => {
    // ベースURL。リクエストごとに変わらない部分
    const baseUrl = 'https://hoge.fuga.com';

    // HTMLデータを取得
    const { $ } = await httpClient.fetch(baseUrl, { search: `foo`, category: 'bar' });
}

main();
```

### 画像のダウンロード
[公式リファレンス](https://www.npmjs.com/package/cheerio-httpcli#-image-element-download-src-attr-) を参考に。

```js
const fs = require('fs');
const client = require('cheerio-httpcli');

// ダウンロードマネージャーの設定(全ダウンロードイベントがここで処理される)
client.download
.on('ready', function (stream) {
  stream.pipe(fs.createWriteStream('/path/to/image.png'));
  console.log(stream.url.href + 'をダウンロードしました');
})
.on('error', function (err) {
  console.error(err.url + 'をダウンロードできませんでした: ' + err.message);
})
.on('end', function () {
  console.log('ダウンロードが完了しました');
});

// 並列ダウンロード制限の設定
client.download.parallel = 4;

const { $ } = await client.fetch(baseUrl, { search: `foo`, category: 'bar' });
// class="thumbnail"の画像を全部ダウンロード
$('img.thumbnail').download();
```

## その他
スクレイピング以外で少しつまったことをまとめてみる。

### URLオブジェクト
Nodeではクライアントjsで普通に使える`URL`オブジェクトがデフォルトでは使えない。
使うには`require('url').URL`としないといけない。

### excelとcsv
今回取得したデータは、csvにしてexcelで読み込むつもりだったが、普通のutf-8だと文字化けしてしまう。
なのでBOM(\uFEFF)をcsvファイルの先頭に追記することで読み込ませるようにした。

## 感想
スクレイピング自体は、参考文献が多くてそんなに苦労しなかったが、取得したHTMLから必要な情報を取得して整理するのがめちゃくちゃめんどくさかった。