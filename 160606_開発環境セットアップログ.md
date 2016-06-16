# ローカル開発ツール セットアップ結果

参考
[02.ローカル開発ツール](https://sites.google.com/a/mynet.co.jp/bb/01-kai-fa/03-rokaru-kai-fatsuru, "02.ローカル開発ツール")

##セットアップ項目

* [Java](#java)
* [Teraterm](#teraterm)
* [Maven](#maven)
* [Ant](#ant)
* [WinSCP](#winscp)
* [MySQL](#mysql)



## <a name ="java">Java</a>

##### セットアップ内容

pleiadesのversion7でpathを通した

## <a name ="teraterm">Teraterm</a>

##### セットアップ内容

ダウンロード

##### 用途

* SSHクライアント

## <a name ="maven">Maven</a>

##### セットアップ内容

インストールしてパスを通した

##### 用途

* antより複雑なビルドに向いてるらしい
* プロジェクト管理ツール機能を持つ

## <a name ="ant">Ant</a>

##### セットアップ内容

インストールしてパスを通した

##### 用途

* ビルドツール
* 複雑な依存関係にあるライブラリの扱いに向いていない
* Mavenにとって変わられつつある

## <a name ="winscp">WinSCP</a>

##### セットアップ内容

ダウンロード

##### 用途

* FTP、FTPS、SFTPクライアント
* サーバーのファイル操作を行うためのプログラム

## <a name ="mysql">MySQL</a>

##### セットアップ内容

インストールしてパスを通した

##### 用途

* ビルドに必要らしいがなぜ必要なのかは見つけることができなかった


***

### セットアップ確認ログ

~~~
$ javac -version
>> javac 1.7.0_80
~~~

Maven

~~~
$ mvn --version
>> Apache Maven 3.2.5 (12a6b3acb947671f09b81f49094c53f426d8cea1; 2014-12-1
>> 3+09:00)
>> Maven home: C:\apache-maven-3.2.5\bin\..
>> Java version: 1.7.0_80, vendor: Oracle Corporation
>> Java home: C:\pleiades\java\7\jre
>> Default locale: ja_JP, platform encoding: MS932
>> OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"
~~~

Ant

~~~
$ ant -version
>> Apache Ant(TM) version 1.8.4 compiled on May 22 2012
~~~

MySQL

~~~
$ mysql> select version();
>> | version() |
>> |:-         |
>> |5.5.50     |
~~~
