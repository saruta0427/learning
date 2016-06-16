# Unixコマンド

## tree

CentOSではインストール作業が必要
`$ sudo yum install tree`

`$ tree | less`

「|」（パイプ）　は画面に表示されるものを右側のコマンドに渡す記号
ここではtreeの結果をlessで表示させている。

## man

コマンドのオプションを調べるためのコマンド
こちらもCentOSではインストール作業が必要
`$ sudo yum install man`

参考
[CentOS(6.4)でmanコマンドやmanページをインストール](http://hyperneetprogrammer.hatenablog.com/entry/2014/07/14/160857)

## ディスク残容量

### df
ディスクの空き容量がわかる

### du
ディスクの使用容量がわかる

### ディスク容量が減り続ける原因は
考えられる理由

- 新しいファイルが生成されている
- 既存のファイルのサイズが大きくなっている

#### 今から15分間に更新されたファイル
`find -mmin -15`

### ログがないどうしよう

もしデーモンが
＿人人人人人人＿
＞　突然の死　＜
￣Y^Y^Y^Y^Y￣
してログもない場合

#### strace

こちらも例に漏れずCentOSではインストール作業が必要
`$ sudo yum install strace`

標準エラーをファイルに出力
`$ sudo strace -f /etc/rc.d/init.d/httpd start 2 > /tmp/trace`
2は標準エラー

### ディスクイメージが消えた場合

VM起動中は何とかなる
ディスクをコピーして復旧

#### lsof

現在開いているファイルを表示する。

あとはgrepでフィルタしてcpでゴニョゴニョする


## 強いコマンド集1
|command|description|
|:-|:-|
|find|検索する|
|xargs|渡された出力を別のコマンドへ渡す｜
|rm|ファイルを削除する|

## 強いコマンドを使った例

### delを含むファイルの削除
`$ find ./hogedir -name "*del*" -print | xargs rm`

### 別のサーバーにバックアップ

`$ tar zcvf - ./backupdir/ | ssh username@127.0.23.2 "cat - > /tmp/send.tgz"`
tarでバックアップファイルのアーカイブを作って送る

## 強いコマンド集2
|command|description|
|:-|:-|
|grep|特定文字列を出力する|
|awk|テキスト処理|
|sort|文字列並べ替え|
|uniq|重複文字列をまとめる|

###

`$ cat access_log | grep "10 Apr 2013 12" | awk '{ print $11}' | sort | uniq -c | sort -nr`
まずaccess_logから"10 Apr 2013 12"が含まれた行を抽出
次にawkでスペース区切りの11番目の文字列を出力
次にsortで同じ文字列どうしで並べ替えた後uniq -c 後で集計
最後に数字が大きい順に並び替え

```
1234 http://mynet.co.jp/hoge/far.html
 123 http://mynet.co.jp/hoge/foo1.html
  12 http://mynet.co.jp/hoge/foo2.html
   1 http://mynet.co.jp/hoge/foo3.html
```

## Linuxモニタリング復習

### CPU負荷

#### top

負荷が高い順に表示される

```
PID  USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
4054 vagrant   20   0 15012 1276 1004 R  0.3  0.2   0:00.10 top
```

こんな感じ
Sはstateつまり状態を表している

Rは使用中
DはIO完了街　この前後で何かボトルネックがある
Sはイベント待ちだったりスリープ中だったり

#### vmstat
色々解析できる
詳しくは↓参照
[vmstat コマンドの読み方](https://blogs.oracle.com/yappri/entry/vmstat)

#### free
メモリの使用率を把握
swapとか見よう

#### iostat
ストレージ負荷を把握する
CentOSに初期状態では入ってない
`sudo yum install iostat`
限界に近いかとかを見とく


#### vnstat
帯域使用状況を取得
これもCentOSにはry)
`sudo yum install vnstat`

## まとめ

ボトルネックの見極めは簡単じゃないのでがんばりましょう
