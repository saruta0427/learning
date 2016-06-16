# Java入門

初めて知ったこと
特に重要そうなことをTIPS形式でまとめました

### プログラムを実行する流れ

ソースコード
↓
コンパイル
↓
インタプリタが実行

#### 定数宣言
final 型

#### 文字列の比較は==ではできない
if(s.equals("hoge")){
とやる

#### 配列要素の作成
int[] score;
score = new int[5];
int[] score2 = {20, 30, 40};

#### メモリと配列
最初に配列をメモリ上につくる
つぎに変数に配列の先頭のアドレスを代入する
参照型なので変数に代入するときは注意

#### Javaはガベージコレクションを勝手にやってくれる

### メソッドの定義

`
public static void hello()
`
アクセス修飾詞 + 静的 + 返り値の型 + メソッド名

```
public static int add(int x, int y){
  int ans = x + y;
  return ans;
}
```

#### オーバーロード
同一メソッドが複数ある場合は引数で判断される
型や引数の個数などでマッチ

#### 他クラスメソッドの使い方

CalcLogicクラスaddメソッドを使いたいときは
CalcLogic.add();

#### JVMは起動時にmainメソッドを呼び出す
最初に実行するクラスファイルにはmainメソッドが含まれていなければならない

#### パッケージ
ソースコードの先頭に記載
`
package calcapp.main;
`

パッケージに階層関係はない
`
CalcLogic.add()
`

これは自パッケージのクラスを読み込んでいる
別のパッケージのクラスを読み込むときは
`
calcapp.logics.CalcLogic.add();
`

という風によぶ

#### importでcallを短縮

```
import calcapp.logics.CalcLogic;
CalcLogic.add();
```

#### すべてのクラスをインポート
`
import calcapp.logics*;
`

#### Java APIは自動でimportされたクラスの集まり
System.out.println()は
java.lang.Systemをimportしたものだった

#### クラス内変数を指定するときはthisをつける

#### 命名ルール

クラス名は単語の頭が大文字
フィールド名、メソッド名は最初以外の単語の頭が大文字

#### クラス型変数
インスタンスを識別できる
継承にも使う

#### インスタンスの生成
ClassName varName = new ClassName();
メモリを新たに確保してインスタンスを生成

#### インスタンスフィールドにアクセス
h.name = "minato";
h.hp = 100;

#### コントラクタ
インスタンスが生成されたときに児童で呼び出されるメソッド

コントラクタになる条件

- メソッド名=クラス名
- 戻り値が記述されていない

```
public class Hero {
  int hp;
  void attack() {
    ....
  }
  Hero() {
    this.hp = 100;
  }
}
```

#### static はインスタンスがなくても呼び出せる

## カプセル化

#### アクセス制御

|修飾詞|アクセス範囲|
|:-|:-|
|private| 自クラスのみ|
|package private| 自分と同じクラス|
|protected |自分と同じパッケージまたは自分を継承したクラス|
|public |すべてのクラス|

定石
フィールドはprivate
メソッドはpublic
クラスはpublic

#### メンバフィールドはクラス内メソッドで操作
setter/getter

### 継承

機能を増やすかんじ

```
public class SuperHero extends Hero {
  private boolean flying;
  public void fly() {
    thie.flying = true;
  }
}
```

差分メンバ

継承したものを更に継承する多重継承も可能
名前がかっこいい

#### 親インスタンスへのアクセス

- 親インスタンスのフィールドを利用

  super.fieldName

- 親インスタンスのメソッドを利用

 super.methodName();

孫インスタンスが祖父母インスタンスに直接アクセスは不可
