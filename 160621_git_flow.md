# Git flow

Git Flowとはいい感じのブランチ戦略

## これだけGit flow

まずmasterブランチからdevelopブランチを作成  
つぎにdevelopブランチからfeatureブランチを作成

```
featureブランチで小単位の作業をする  
小単位の作業が終わったらdevelopにマージ  
```

これを繰り返して実装をする  
終わったらreleaseブランチにマージして最終チェック、バグ修正  
releaseブランチでの確認作業が終わったらmasterにマージ  
リリース後、緊急自体が起きたらhot-fixブランチを使い開発作業  
終わったらhot-fixをmasterとdevelop両方にマージ

## Source Treeの使い方  

Source Tree Ver 1.6  

`Git Flow → 新規フィーチャーを開始`  
ここでdevelopブランチも自動的に作成される

```
 developブランチが作れないとき  
 `$ git flow init`
```

`Git Flow → フィーチャーをブランチを完了`  
developにマージしてフィーチャーブランチは消える

## TIPS

### ブランチを削除するときの注意  

現在のブランチを削除しようとするとエラーが出て削除できない    
他のブランチにチェックアウトすることで削除できるようになる  
