---
title: Hexoでの初めてのブログ構築
date: 2019-02-21 18:59:41
tags:
- Hexo
categories: 技術
---


## Hexoのダウンロードと初期起動
{% codeblock  lang:sh %}
npm install -g hexo
hexo init test_dir
hexo server
{% endcodeblock %}
まず`npm install -g hexo`でhexoをグローバルインストール。
`hexo init test-dir`で新規にhexoプロジェクトの作成。
`hexo server`でサーバー立ち上げと表示。

## テーマ変更
今回使うテーマは[simple-japanese](https://github.com/mitsuruog/hexo-theme-simple-japanese)
基本的にはここの`README`にあるように進める。

1. `git clone https://github.com/mitsuruog/hexo-theme-simple-japanese.git themes/simple-japanese`でダウンロード。
このときgit管理したい場合はzipでダウンロードしたりgitの`submodule`使ったり(よくわかってない)する。
1. `_config.yml`を書きかえ

```yml
# Site
author: YOUR_NAME
author_title: YOUR_DESCRIPTION
avatar: YOUR_AVATAR_URL

# URL
url: YOUR_BLOG_URL

theme: simple-japanese

# Sidebar
widgets:
  - search
  - profile
  - recent_posts
  - tagcloud
  - archive

# Contact
contact:
  url: YOUR_CONTACT_URL
  icon: github # font-awesome icon. e.x) fa-github

# Google tag manager
google_analytics: GTM-XXXXXX

# Custom assets
simple_japanese:
  custom_assets:
    css: css/custom.css
    js: js/custom.js
```

## アーカイブの書式変更
デフォルトだとこのテーマのアーカイブは`二月 2019`のようになっていて、漢数字がすごくダサイ。
hexoには[ヘルパー](https://hexo.io/docs/helpers)というejsで使える関数がいろいろ用意されているみたいなのでそれを利用する。

`themes\simple-japanese\layout\_widget\archive.ejs`の中は以下のような記述になっている。
```js
<% if (site.posts.length){ %>
<div class="widget-wrap">
  <h3 class="widget-title"><%= __('widget.archives') %></h3>
  <div class="widget">
    <%- list_archives() %>
  </div>
</div>
<% } %>
```

この中の`list_posts()`を例えば`list_archives({format:'YYYY/MM'})`のように書きかえると、`2019/02`のように表示されるようになる。
その他のオプションは[公式ドキュメント](https://hexo.io/docs/helpers.html#list-archives)参照


## その他自分用まとめ
* configの`widget`にwidgetの中にあるejsファイルを指定すると出してくれる
* `<%= __('index.category') %>`といった感じにすると、`ja.yml`にあるものが表示される
* `source/css`にあるstylファイルでレイアウトをいじくれる。importを忘れずに
* `layput/category.ejs`を作成し、`layout/_patial/archive.ejs`を修正するとカテゴリページをカスタマイズできた
* fontawsomeの導入 `_patial.head.ejs`にCDNで読み込み
* [ここ](https://hexo.io/docs/variables)が割と便利。ejsで使える変数などがまとまってる
* 画像はconfigいじったら、投稿ごとのフォルダにまとめれるらしい
* `hexo-browsersync`プラグインでオートリロード
* `hexo clean`でキャッシュやpublicフォルダの削除

### favicon
`_config.yml`に`favicon: /favicon.ico`と追加し、`/source`直下にfavicon設置でOK

### シンタックスハイライト
[ここ](https://hexo.io/docs/tag-plugins)参照

```
{% codeblock lang:sh %}
cd Homestead
{% endcodeblock %}
```

こんな感じにするとハイライトされた

## 参考
* [Hexoでローカルに静的なブログを作ってみて基本構成を把握する](https://tech.qookie.jp/posts/info-hexo-local/)
