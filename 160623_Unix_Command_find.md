findことはじめ　　

findはデフォルトではディレクトリを検索する　　
ファイルもディレクトリもまとめて検索  
`$ find ~/dir -name "pattern"`

ファイルだけ見つけたい(ディレクトリはd)
`$ find ~/dir -name "pattern" -type f`

オプション多すぎてどうやってまとめられれば

最近変更されたファイルを探す
-amin アクセス時刻
-atime
-type f or d
-name "pattern" //基本はワイルドカードを使った検索に使う
1日以内に更新されたものを探す  
`$ find ./ -mtime -1`

1日前、以前にアクセスされたものを探す  
`$ find ./ -atime +1`

-anewer file
指定したファイルより後にアクセス

### アクセス時刻で検索

### 更新時刻で検索

### ステータス変更時刻

### 時刻検索