# gitの基本的なコマンドまとめ

## 変更をステージに追加
* `git add .` 「.」は全てを追加の意味。
* `git add ファイル名`
* `git add ディレクトリ名`

## 変更を記録（コミット）
* `git commit -m"メッセージ"`　エディタを立ち上げずにメッセージを送れる
* `git commit -v` エディタを立ち上げて、変更内容を打ち込める

### コミットメッセージの書き方
* 簡単に書くとき：変更内容の要点と理由を１行で書く
* 正式に書くとき：１行目に変更内容の要約、２行目に空白、３行目に変更した理由

## 現在の変更状況の確認（addしたか、comittしたかの確認）
* `git status`

## 変更の差分を確認する
### addする前の変更差分の確認
* `git diff`
* `git diff ファイル名`

### addした後の変更差分の確認
* `git diff --staged`

## 変更履歴の確認
* `git log`
* `git log --oneline` 1行で表示
* `git log -p index.html` ファイルの変更差分を表示
* `git log -n コミット数` 表示するコミット数を制限

## ファイルの削除
* `git rm ファイル名`
* `git rm -r ディレクトリ名`
* 上記の方法では、ワークツリーからも消え、gitの記録からも消える。
* リポジトリからだけ消したい場合は以下
* `git rm --cashed ファイル名`

## リモートリポジトリを新規追加
* `git remote add origin https://~`

## リモートリポジトリへ送信
* `git push origin master`

## コマンドにエイリアスをつける
example
* `git config --global alias.cm commit` 「commit」を「cm」で使えるようにした。

## リモートの表示
* `git remote` 設定しているリモートリポジトリの名前を表示

## リモートからのプル
* `git pull リモート名 ブランチ名`

## リモートの削除
* `git remote rm リモート名`

## ブランチの作成
* `git branch ブランチ名`

## ブランチの一覧を表示
* `git branch` ブランチの一覧を表示
* `git branch -a` リモートリポジトリも表示

## ブランチの切り替え
* `git checkout 既存ブランチ名`

## 変更履歴をマージ
* `git merge ブランチ名`

## ブランチの削除
* `git branch -d ブランチ名`

## githubを使った開発の流れ(Github ver)
1. 自分のブランチを作成
2. ファイルの変更
3. `git add .`する
4. `git commit -v`
5. gitプッシュ　`git push origin` 作業用ブランチ (ここまでがローカルの作業ブランチ内での作業。次がGithubでの作業)
6. Githubの＜code＞の画面でbranchを自分の作業用ブランチに切り替える
7. New pull requestを押す
8. メッセージを書く **compareを作業用ブランチになっているか確認**
9. 緑のCreate Pull requestボタンを押す
10. Merge pull request を押す（１０、１１は共同開発なら誰か他の人がやる）
11. Confirm mergeを押す（プルリクが終了）
12. ローカルで自分のブランチをmasterにして、リモートの内容をローカルにpullする。`git pull origin master`
13. ローカルのブランチを作業用ブランチに切り替え、masterの内容を開発ブランチにmergeする。`git merge master`
