---
title: Laravel Homestead環境の構築
date: 2019-02-24 11:28:43
categories: 技術
tags:
- Laravel
- Vagrant
- Homestead
---

今までxamppでLaravel環境を構築していたが、業務でVagrantを使っていい機会なのでLaravel Homestead環境を構築してみた。

**目次**
<!-- toc -->

## Homesteadのインストール
まず、Homesteadのboxをダウンロードする。  
その際どの仮想環境を使用するか聞かれたので、VirtualBoxを選択。  
自分の環境では  30分くらいかかった。
{% codeblock lang:bash %}
vagrant box add laravel/homestead
{% endcodeblock %}

そのあと、homesteadリポジトリをcloneし、自分が使いたいバージョンのブランチにチェックアウトする。
最後に初期化batを走らせて環境構築終了。
{% codeblock lang:bash %}
git clone https://github.com/laravel/homestead.git ~/Homestead
cd ~/Homestead
git checkout v7.18.0
init.bat
{% endcodeblock %}

## Homestead.ymlの編集
ymlを編集するが、その前にssh鍵がない場合は作成する。
何か聞かれてもEnter連打でOK
{% codeblock lang:bash %}
cd ~/
ssh-keygen -t rsa
{% endcodeblock %}

その後`Homestead.yml`を編集する。
{% codeblock Homestead.yml lang:yml %}
ip: "192.168.10.10" #接続先となるIPアドレス
memory: 2048 #割り当てるメモリ(MB)
cpus: 1 #同CPUのコア数
provider: virtualbox #VMのホスト

authorize: ~/.ssh/id_rsa.pub #SSH公開鍵の場所

keys:
    - ~/.ssh/id_rsa #秘密鍵の場所

folders:
    - map: ~/code #ローカルのディレクトリ
      to: /home/vagrant/code #VM上のディレクトリ

sites:
    - map: projectName.local #ホスト名
      to: /home/vagrant/Code/projectName/public #公開するディレクトリ

databases:
    - homestead

{% endcodeblock %}

ついでにhostsファイル(C:\Windows\System32\drivers\etc\hosts)も編集しておく。
{% codeblock hosts%}
192.168.10.10  projectName.local
{% endcodeblock %}


## プロジェクトの作成
Laravelプロジェクトを作成するためにまずはVagrant環境にログインする。
{% codeblock ホスト lang:bash %}
vagrant up
vagrant ssh
{% endcodeblock %}

ただし、自分の環境では[ネットワークの設定エラー](https://qiita.com/7968/items/97dd634608f37892b18a#%E3%82%A8%E3%83%A9%E3%83%BC1%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%82%A8%E3%83%A9%E3%83%BC)と同じエラーが出た。  
なので`Homestead.yml`と`hosts`のipを例えば`192.168.30.10`のように変更するとちゃんと動いた。


そのあと、プロジェクトの作成。ホストのディレクトリは作っておく。
{% codeblock ゲスト lang:bash %}
cd ~/code
composer create-project laravel/laravel projectName
{% endcodeblock %}

そして、ブラウザで http://projectName.local を開いて、初期画面が表示されれば成功。

## DBの変更
データベース名などを変更したいときは、`Homestead.yml`を編集する。複数もOK
{% codeblock Homestead.yml lang:yml %}
databases:
    - homestead
    - projectName
    - sample
{% endcodeblock %}

変更したら、`vagrant reload --provision`を実行すると反映される。

## DBへの接続
vagrant上のデータベースの確認には[A5:SQL Mk-2](https://a5m2.mmatsubara.com/)を使う。
.envの情報をもとにA5からデータベースにアクセスする。
`データベース > データベースの追加と削除 > 追加 > MySQL（または PostgreSQL）`
{% codeblock .env lang:yml %}
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
{% endcodeblock %}

その際に、`socket error code 10061`というエラーで接続できないことがある。
そのときは、[Windows上のvagrantにMySQLやらPostgreSQLのクライアントにA5SQLを使う](http://snowlong.hatenablog.com/entry/2017/07/10/160324)を参考にトンネル経由で接続するとうまくいった。

 ## 参考
* [Laravel開発のはじめかた Windows編](https://www.hypertextcandy.com/start-laravel-project-on-windows)
* [Laravel Homesteadに複数のプロジェクトを構築する方法](https://www.hypertextcandy.com/multiple-projects-in-laravel-homestead)
* [Laravel Homestead 公式](https://readouble.com/laravel/5.7/ja/homestead.html)
* [【Laravel超入門】開発環境の構築（VirtualBox + Vagrant + Homestead + Composer）](https://qiita.com/7968/items/97dd634608f37892b18a)