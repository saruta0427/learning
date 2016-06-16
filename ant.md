# ant

build-release.xml
- property, conditionがスペースインデント
- 59行目にスペースが混じってる

## プロジェクト

|attribute|description|required|
|:-|:-|:-|
|name|プロジェクト名||
|default|省略時は"main"がデフォルトターゲット|no|
|basedir|省略時はこのビルドファイルがある場所がベース|no|

## プロパティ
プロジェクト内変数
`<property name="srcdir" value="./src"`
${srcdir} が ./src に置換される。

## コンディション
条件に一致した場合はプロパティに値をセットする。

## ターゲット
タスクの集合

|attribute|description|required|
|:-|:-|:-|
|name|ターゲット名|yes|
|depend|依存するターゲット|no|
|if|実行に必要なプロパティ|no|
|unless|実行に必要なプロパティ|no|
|description|ターゲット機能の説明|no|


M2リポジトリーの決定
たぶんファイル参照先？

## タスク

### タスクコマンド

|attribute|description|required|
|:-|:-|:-|
|replace|指定したファイルの文字列を置換||

### 汎用的な属性

|attribute|description|required|
|:-|:-|:-|
|failonerror|エラーが発生した際ビルドを中断するか否か|no|
|excludes|除外するファイルのパターンリスト|no|



\ <!-- Wicketを本番モードに変える -->
Wicketってなんぞ？
development を deploymentに置換
