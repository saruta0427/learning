# sa

学ぶこと
- 各種APIの知識
- 設計理論や開発ツール
- チーム開発方法論や開発手法

#### 文字列調査
equalsには大文字小文字を区別するメソッドと気にしないメソッドがある
文字列連結はできるだけ演算子+を使わないでやる

#### StringBuilder

```
StringBuilder sb = new StringBuilder();
for(int i = 0; i < 10000; i++) {
  sb.append("Java");
}
String s = sb.toString();
```

基本は StringBuilder
使えない場合は StringBuffer

#### 正規表現

##### matches()メソッド
`
name.matches("[A-Z][A-Z0-9]{7}")
`

他の正規表現メソッド
`
split() replaceAll()
`

##### プレースフォルダを使ったformat()使ったメソッド
```
final String FORMAT = "%8s %6s 所持金%,5d";
String s = String.format(FORMAT, hero.getName(),
                                 hero.getJob(),
                                 hero.geGold()
);
System.out.println(s);
```

% + 修飾 + 桁 + 型

|修飾詞||
|:-:|:-|
|,|3桁ごとにカンマ|
|0|空き領域0 fill|
|-|左寄せ|
|+|符号強制表示|

桁
表示をそろえるために使う

### コレクション

- 単独格納

  - List
  順番に格納

  - Set
  順序があるとは限らない

- ペア格納

  - Map
  Key Value


#### ArrayList
配列と似てる
ArrayList<String>
<>を使った表現をジェネリックと呼ぶ

ArrayListのいいところ
- サイズ指定がいらない
- しかし配列の方がメモリ効率がいい

ArrayListにはインスタンスでないものは格納できない


##### Javaのforeach
```
for(String s: array){
  ~
}
```

##### イテレータ
カーソルみたいなもの

|             |ArrayList|LinkedList|
|:------------|:-------:|:--------:|
|要素の挿入削除|    ×    |     ○    |
|要素の取得    |    ○    |     ×    |

#### Mapの使い方
Key Valueペア
String型のキーとInteger型の値をペアに格納する場合は、
Map<String, Integer>型と表現

### インスタンス5大基本操作

#### インスタンスの文字列表現

toString()メソッドの責務
クラスを作った人がオーバーライドして適切な文字列を返すようにする

#### インスタンスの等価判定

equals()メソッドのオーバーライド
二つのクラスは何をもって等価といえるのか
その基準を定義

#### インスタンスの要約

自動で生成されるハッシュ値は適切とはいえない
いえない自分でオーバーライド自分でする

#### インスタンスの順序づけ

compareTo()
これで定義した値を使って使って大小関係を比較ソートする

#### インスタンスの複製

インスタンスは変数定義でコピーされない
```
Hero h1 = new Hero("minato");
Hero h2 = h1;
```

clone()メソッドを使う
```
Hero h1 = new Hero("minato");
Hero h2 = h1.clone();
```

Cloneableインターフェースを実装する必要あり

### さまざまな種類のクラス

#### 列挙入らない型宣言

```
enum AccountType {
  FUTSU, TOUZA, TEIKI;
}
new Account("1732050", AccountType.FUTSU);
public class Account {
  private String accountNo;
  private int balance;
  private AccountType accountType;
  public Account(String aNo, AccountType aType) {...}
}
```

列挙型により特定の値以外入らないようにする

#### 外部プログラムの実行

##### ProcessBuilderクラス
```
ProcessBuilder pb = new ProcessBuilder(
  "c;\\window\\system32\\notepad.exe"
);
pb.start();
```

### 非標準ライブラリの活用

クラスパスは直下のクラスしか読み込まない
ライブラリであるjarファイルをインクルードするときは
~/hoge.jarをクラスパスに設定する必要がある

### ファイルの操作

#### テキストファイルの読み書き

##### FileReader
テキストファイルの先頭か最後に文字を追加できる

##### FileOutputStream
扱うデータは文字ではなくバイト
これいつ使うん？

##### ファイルの閉じ忘れ
ほかのプログラムから読み書きやファイルが開けなくなったりする
エラーとかで閉じる処理がきちんとされない可能性もある
あるきちんと例外処理をする

#### ストリーム

すこしずつファイルの読み書きをすること
ファイルが大きすぎてメモリに乗らない
JVM外部のデータの大きさは事前にわからない
わからない少しずつ読み書きするのが無難

#### フィルタ
ストリームに付加的に接続するための道具
多種多様な変換をする

##### バッファリングフィルタ
ストリームデータを溜め込み、まとまった量になったら下流に流す
書き込み回数を減らすことができる

### さまざまなファイル形式

#### プロパティファイル
key,valueファイル形式
すべて文字列として取得

#### XML
ネスト構造のデータストックに対応
HTMLに似た記法
セレクタのような方法で呼び出しできる

## ネットワーク通信

java.net.URL通信クラスを使う
```
URL url = new URL("http://hogehoge.jp")
InputStream is = url.openStream();
```

### Socket通信

```
// socketインスタンス
Socket sock = new Socket("hogehoge.jp", 80);

// 入出力ストリーム取得
InputStream is = sock.getInputStream();
OutputStream os = sock.getOutputStream();

// 読み書き
int i = is.read();
os.write("HELLO");

// socket閉じる
sock.close();
```

#### ServerSocket例
```
// ポート36921で町受けするソケットインスタンス
ServerSocket svSocket = new ServerSocket(36921);

Socket sock = svSock.accept();
```

## 単体テスト

単体テスト用にmain()メソッドの入ったクラスを作る

作るべきテストケース
自然数が入るべきところに負の数を入れてみたりNULLを入れてみたり

テストケースの見つけ方
- 同値分割
- 境界値分析

JUnitなどのテスティングフレームワークの活用

稼動クラスを作りながら並行でテストケースを作った方が品質がよくなるということが経験で知られている

#### アサーション
ソースコード内に直接てすとケースを記述できる
下記のコードはbalanceが0未満であるときにエラーメッセージを表示するもの
`
assert this.balance >= 0;
`

ゼッタイに起こってはならない異常事態に備える保険
単体テストの代わりにはならない

#### リファクタリング
仕様を変えずにコードを修正
リファクタリングの後には再度同じテストをする

リファクタリング箇所を定めるためには
静的コード解析ツールを使うといいらしい

## チーム開発

### UML-統一モデリング言語
図の名称の統一規格

### アジャイル
アジャイルが活きる場面
コミュニケーションが密
チームの士気が高い
少数精鋭
大規模な場所では難しい

### テスト駆動開発
最初にテストケースを記述して
最小限の努力でテストが通るクラスを開発する。

### スクラム
アジャイル開発一つ

### ビルドの自動化

継続的インテグレーションでは高い頻度でコンパイルやテストを繰り返す。
一連の作業を一回のコマンドで実行できると楽。

### ant
処理手続きの記述

### Maven
最終的なゴールを定めそれを目指す
