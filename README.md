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

## ファイルの削除を記録する
* `git rm ファイル名`
* `git rm -r ディレクトリ名`
* 上記の方法では、ワークツリーからも消え、gitの記録からも消える。
* ワークツリーには残したいけど、リポジトリ（gitの記録）からだけ消したい場合は以下
* `git rm --cashed ファイル名`

## ファイルの移動を記録する
* `git mv 旧ファイル名 新ファイル名`
* これは以下のコマンドと同じ意味
* mv 旧ファイル名 新ファイル名
* git rm 旧ファイル名
* git add 新ファイル名

## リモートリポジトリを新規追加
* `git remote add origin https://~`

## リモートリポジトリへ送信
* `git push origin master`
* `git push リモート名 ブランチ名`

## コマンドにエイリアスをつける
example
* `git config --global alias.cm commit` 「commit」を「cm」で使えるようにした。

## ファイルをgitに追跡させない
* `.gitignore`ファイルを作成し、そこに、gitで追跡させたくないファイル名を書き込むと、指定したファイルはgitに追跡されない。パスワードなどが記載されているもので使う。

## ファイルへの変更を取り消す
* `git checkout -- ファイル名`
* `git checkout -- ディレクトリ名`
* `git checkout -- `：全変更を取り消す
* 裏側：ワークツリーをステージと同じ状態にするという処理

## ステージした変更を取り消す
* `git reset HEAD ファイル名`
* `git reset HEAD ディレクトリ名`
* `git reset HEAD`　：全変更を取り消す
* 指定した変更をステージから取り消すだけなので、ワークツリーのファイルには影響を与えない。

## 直前のコミットをやり直す
* `git commit --amend`
* リモートリポジトリにPushしたらコミットはやり直ししてはいけない。
*　まず、ファイルを修正し、`git add .`、それから`git commit --amend`

## リモートの表示
* `git remote` 設定しているリモートリポジトリの名前を表示
* `git remote -v` 対応するURLを表示

## リモートからの情報取得する2つの方法
1. fetch：`git fetch リモート名`　ローカルリポジトリに情報が落とされ、ワークツリーには落とされない。ワークツリーに反映させたいなら、`git merge`する必要がある。
2. pull：`git pull リモート名　ブランチ名`　例`git pull origin main` リモートから情報を取得して、マージまでを一度にやりたい時。これは、`git fetch origin main` `git merge origin main`と同じ操作。
* pullは挙動が特殊なので、基本的にはfetchを使うのがおすすめらしい。
* プルの注意点：今いるブランチにマージされてしまうので、注意が必要。

## リモートの詳細情報を表示する
* `git remote show リモート名`

## リモートの削除
* `git remote rm リモート名`

## リモート名の変更・削除
* `git remote rename 旧リモート名　新リモート名`

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

## githubの流れ
1. githubで新規のリポジトリを作成
2. URLをコピーし、`git remote add ブランチ名？ URL`で
3. `git push リモート名 ブランチ名`で変更内容をリモートに反映させる

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
