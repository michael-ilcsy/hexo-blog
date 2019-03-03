---
title: PhpStormの導入 <インストール&キーバインド編>
date: 2019-03-03 23:05:48
tags:
- PHP
- PhpStorm
categories: 技術
---

今までVScodeをカスタマイズして使っていたが、PHPを書くのに辛くなってきたのでPhpStormを使い始めることにした。
設定等がかなり書くことが多くなりそうなので、今回はインストールとキーバインドまでにする。

**目次**
<!-- toc -->

## PhpStormのインストール
基本的には公式のヘルプを見ると大体分かる。
[PhpStormのインストールとセットアップ](https://pleiades.io/help/phpstorm/install-and-set-up-product.html)

## 日本語化
日本語化も丁寧に解説してくれているところが多く特に詰まることはないと思う。
[JetBrains 製品の日本語化マニュアル](https://pleiades.io/pages/pleiades_jetbrains_manual.html)
[PhpStormの日本語化(Windows環境・Pleades利用）](https://qiita.com/tmak_tsukamoto/items/95a32a1d36094cb44f1b)
[PhpStormの日本語化](https://macha795.com/phpstorm-japanese/)

## 個人的によく使うショートカット
一般的なものや他のエディタ等と一緒のものは除いています。

|ショートカット|アクション|
|:---|:---|
|Ctrl + z|**Undo**<br>やり直し|
|Ctrl + Shift + z|**Redo**<br>元に戻す
|Ctrl + y|**Delete Line**<br>行を削除<br>VScodeは元に戻すなので、間違えるとどんどん行が消えていく<br>(10回ぐらいやらかした。)
|Ctrl + d|**Duplicate line or Block**<br>行を複製
|Alt + Insert|**Generate**<br>Getter,Setter,コンストラクタ,PHPDocなどを生成
|Ctrl + /|**Comment with Line Comment**<br>行コメントを挿入・削除
|Ctrl + →<br>Ctrl + ←|**Move Caret to Next/Previous Word**<br>単語単位で右/左に移動
|Alt + ↓<br>Alt + ↑|**Next/Previous Method**<br>次/前のメソッドに移動
|Ctrl + n|**Navigate Classt**<br>クラス名でファイルをインクリメンタル検索<br>SCと入力するとSampleClassがヒットします。
|Ctrl + Shift + n|**Navigate File**<br>ファイル名でファイルをインクリメンタル検索<br>s_cと入力するとsample_classがヒットします。
|Ctrl + Alt + Shift + n|プロパティ、メソッド名、クラス名などでファイルをインクリメンタル検索
|Ctrl + b|**Navigate Declaration**<br>定義に移動<br>**これがないとやっていけないくらい超必須級**
|Ctrl + Shift + i|定義をpeek(ポップアップウインドウのようなもので見れる)
|Ctrlを押しながらカーソル|ツールチップ表示
|Ctrl + f|**Find**<br>ファイル内で文字列を検索
|Ctrl + Shift + f|**Find in Path**<br>プロジェクト内で文字列を検索
|Ctrl + r|**Replace**<br>ファイル内の文字列を置換
|Shift + F6|**Refactor Rename**<br>クラス名・メソッド名を変更<br>**使用している箇所を一括で置換します。そこそこ使う**
|Alt + →<br>Alt + ←|**Select Next/Previous Tab**<br>右/左のタブに移動
|Esc|**Go to Editor**<br>エディタに移動。ターミナルなど移動できないものもある<br>**使用頻度高め**
|Alt + 1|**Tool Windows Project**<br>プロジェクトウインドウへ移動
|Alt + 5|デバッグウインドウを開く
|Alt + F12|ターミナルを開く
|Alt + F12|ターミナルを開く
|Ctrl + Shift + x|コマンドラインツールの入力欄にフォーカス
|Ctrl + r|**Replace**<br>ファイル内の文字列を置換
|Ctrl + Shift + Enter|行末のセミコロンなども含めてステートメントを補完してくれる。<br>`function hoge -> function hoge(){}`<br>**めちゃくちゃ使う。必須級**
|Shift二回押し|どこでも検索
|Alt + Enter|電球マークが出ている時に電球マークの内容表示<br>クラスのインポートやfunctionのuseの追加等様々なことに使う。<br>**たぶん一番使ってる。超必須**




### 参考
[PhpStorm 公式ショートカット一覧 (日本語版) Windows/Linux](https://pleiades.io/sites/willbrains.jp/keymap/pdf/shortcut_phpstorm_windows.pdf)
[Windows/Linux版PhpStormのキーボードショートカット](https://www.karakaram.com/phpstorm-keymap-windows)
