# Grep

sample.txtの中身  
```
aaa
bbb
ccc
aaaa
```

## 基本技  

- ### aaaが入った行を抽出する(部分一致)  

  `$ grep aaa sample.txt`  
  ```
  >>> aaa
  >>> aaaa
  ```

- ### or 検索regexp  

  `$ grep -e aaa -e bbb sample.txt`  
  ```
  >>> aaa
  >>> bbb
  >>> aaaa
  ```

- ### 大文字小文字を区別しないignore   

  `$ grep -i aaa sample.txt`  
  ```
  >>> aaa
  >>> aaaa
  >>> AAA
  ```

- ### マッチした行を除くinvert  

  `$ grep -v aaa sample.txt`  
  ```
  >>> bbb
  >>> ccc
  >>> AAA
  ```

- ### マッチした行の後ろの行を指定した数出力する(-Bだとマッチの前)  

  `$ grep aaa -A 2 sample.txt`  
  ```
  >>> aaa
  >>> bbb // 1st
  >>> ccc // 2nd
  >>> aaaa
  >>> AAA // 1st
  ```

- ### マッチした行を持つファイル名を出力　
  ファイル検索用途(L:マッチしないファイル)  
  `$ grep -l aaa *.txt`  
  `>>> sample.txt`  

- ### 再帰的に検索するrオプション  
  ディレクトリ内のファイルを全検索recursive      
  (Rはシンボリックも対象)  
  `$ grep -r aaa dir`  
  ```
  dir/sample.txt:aaa
  dir/sample.txt:aaaa
  ```  
- ### 単語検索 word  
  `$ grep -w aaa　sample.txt`  
  切れ目の判定は英数字とアンダースコア以外  
  aaaaとかaaabはマッチしない  
  ```
  >>> aaa
  ```


## その他のオプション

|option|description|
|:--|:--|
|o|行全体ではなくマッチした部分のみ表示。正規表現を使わないと意味がない|
|c|マッチした回数を表示(count)|
|m|指定した数マッチを表示する。それ以降のマッチは無視|
|n|行番号を表示(number)|
|x|行全体が完全一致|
|H|ファイル名を表示(h:ファイル名を表示しない)|
|b|ファイルの初めから何文字目か表示|

## オプション組み合わせ  

### ディレクトリ内の特定ファイルを検索  
`$ grep -lr .txt$ dir`  


## 正規表現  

|文字|効果|
|:--|:--|
|_|改行文字以外の何か1文字|
|*|直前の1文字のn回|
|^|行の先頭|
|$|行の末尾|
|[]|かっこ内の任意の文字に一致ハイフンで範囲指定も可。最初に^をつけると意味が逆になる|
|+|直前の文字の1個以上の連続|
|?|直前の文字の0または1文字にマッチ|
|pattern1&#124;pattern2|パターン1,2いずれかにマッチ|
|(pattern)|パターンのグループ化|
|￥|正規表現記号を通常の文字列として扱う|
