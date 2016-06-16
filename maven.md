#Maven

antと違って依存関係を何度も記述する必要はない

## ビルド・ライフサイクル

コンパイル→テスト→JAR作成
などのビルドにおける作業の順番を定義したもの

ビルド・ライフサイクルは１つ以上のフェーズを含んでいる
フェーズが実行されるためには一つ前のフェーズが実行済みでなければならない

### pom.xml
さまざまな情報を記録できる
- プロジェクト情報
- 依存関係
- 利用するプラグイン
- ライセンス

### ローカルリポジトリ
JARをインストールしたり

### 依存関係
```
<dependency><!-- このプロジェクトはJUnit バージョン4.12に依存している -->
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
</dependency>
```
### buildの中身

- resource
resourceで定義したファイルをアウトプットディレクトリにコピーする
- compile
コンパイル
- surfire
JUnitを走らせる
- war
warファイルをビルドする
- javadoc
javadocを作る
- site
何に使われているかわからない
- jetty
jettyコンテナを動かす jettyがよくわからない
- tomcat
インストール済みのtomcatでサーバーを起動
- com.google.code.maven-replacer-plugin
よくわからなかった
- yuicompressor-maven-plugin
css, js を圧縮
- maven-filljavascript-plugin
よくわからなかった
- sql-maven-plugin
DBを作る(これはテストであって本番環境には直接的に関係ない)
