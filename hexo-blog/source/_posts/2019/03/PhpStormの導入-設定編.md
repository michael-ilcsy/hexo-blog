---
title: PhpStormの導入 <設定編>
date: 2019-03-04 14:02:13
tags:
- PHP
- PhpStorm
categories: 技術
---

今回は、フレームワークやツールに関係しないPhpStormの一般的な設定について書いていく。

**目次**
<!-- toc -->

## はじめに
基本は[公式リファレンス](https://pleiades.io/help/phpstorm/settings-preferences-dialog.html)に全て書いてあるので、ここを見たら大体のっている。ただ、量が多すぎて見つからないこともあるのは注意。

## 保存系の設定
### 自動保存の無効化
jsでファイル変更を検知してビルドする設定にしていると、自動保存で毎回ビルドされて鬱陶しい。
デフォルトでは、別アプリケーションにフォーカスを切り替えたときに自動保存されるようになっているので、その設定を外す。

[PHPStormのファイルの自動保存機能をオフにして動作を軽くする](https://qiita.com/J_Sugar__/items/1bdc8240c4ff099d96ff)

### ファイルが保存済みかどうか表示する
VScodeなどでは、未保存のファイルはタブに●がついて分かるようになっている。
PhpStormではデフォルトは保存済みか分からないので設定する。

[phpStormでファイルが保存済みかどうかをタブに表示する](http://wigwamania.hatenablog.com/entry/2016/09/23/171123)

### 保存時にフォーマットする
個人的な話だが、保存時にフォーマットされないと発狂してしまう体になってしまっている。
しかし、PhpStormにはデフォルトでそういう設定がないのでごり押しで作った。

詳細はリンクを見て頂きたいが、簡単に説明すると

1. もともと`Ctrl + Alt + s`は設定画面を開くショートカットが割り当てられている。
2. だが、そんなに使わないショートカットなので、`Ctrl + Alt + s`にフォーマットするマクロを登録する。
3. `Ctrl + s`を保存 + `Ctrl + Alt + s`の動作に変更。

ということを行った。

[PhpStormでSave(保存)する再にReformat(再整形)させる方法](http://blog.short-leg.net/program/php/2257/)


## エディタ系の設定
### コード補完時に大文字小文字の区別をしない
デフォルトでは補完時に大文字小文字の区別をされるので、クラスを補完しようとすると最初を大文字にしないと補完対象から外れてしまう。
区別するメリットがほとんどないと思うので、区別しないように設定する。

[PhpStormで、コード補完時に大文字小文字の区別をしない](https://iww.hateblo.jp/entry/20150829/codecompletion)

### 連想配列の矢印を綺麗に整列させる
正直いらないときもあるが、場合によっては整列させたい時もあるので。

[PhpStormで連想配列の矢印を綺麗に整列させる設定](https://www.juku90.com/phpstorm-align-key-value-pairs/)

### キャメルケース、スネークケースなどの切り替えプラグイン
地味にケース変換をよくするのだが、設定になかったのでプラグインを導入した。
`設定 > プラグイン`からダウンロードできる。インストール後は`Shift + Alt + U`でケース変換が可能。

[キャメルケース等の切り替えプラグイン](https://plugins.jetbrains.com/plugin/7160-camelcase)

## その他の設定
### プロジェクトウインドウなどでワンクリックでファイルを開く
デフォルトではプロジェクトウインドウでファイルをダブルクリックしないと開かない。
一長一短だが、ワンクリックで開くほうが嬉しいので設定した。

[ワンクリックでファイルを開く](https://qiita.com/takkyun/items/4d27f43b78f9c71af9b3#project-%E3%83%9A%E3%82%A4%E3%83%B3%E3%81%AE%E8%A8%AD%E5%AE%9A)

### ターミナルの文字化け
SSH Terminalに接続して日本語が文字化ける場合↓

1. 「File」->「Settings」->「Tools」->「SSH Terminal」
1. 「Default encoding」を「UTF-8」に変更。
1.  ターミナルの再起動

で直った。

### ESlintの設定
個人的には`Javascript standard style`が好きなのだが、デフォルトでは使用されないので設定。

[デフォルトとしてJavaScript標準スタイルを設定するには](https://pleiades.io/help/phpstorm/eslint.html#ws_js_linters_eslint_using_JavaScript_Standard_Style)

### 除外フォルダの設定
Laravelのpublicフォルダにあるビルド後のjsファイルなどが、補完やジャンプ対象となるのがうっとうしいので除外設定する。

[名前パターンでファイルとフォルダーを除外する](https://pleiades.io/help/phpstorm/excluding-files-from-project.html#exclude-by-pattern)

---

随時更新予定