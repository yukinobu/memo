# Amplifyセキュリティメモ

## ローカルコンピュータ

### ~/.aws/credential

* amplify configure の際に作成される。
  * プロファイルを default で進めると上書きされるかも？
* 以後使用しないので削除して良い？

### ~/.aws/amplify/deployment-secrets.json

* よく判らない…が、ファイル名からして何かありそう

### ~/.amplify/admin/config.json

* amplify pull の際に作成される
* amplify コマンドがバックエンドを操作するためのトークンが入っている。
* これを盗まれると、バックエンドを不正に操作される恐れがありそう。

## 開発者の追加

* 管理者の操作
  1. Git リポジトリへのアクセスを許可
  2. Amplify Admin UI を有効にして Invite
* 開発者への案内
  1. git clone
  2. Amplify Admin UI にログイン（要PW設定）
  3. amplify pull
     * Amplify Admin UI を使い方法でセットアップすること

## IAM ユーザー

### amplify configure の際に作成したユーザ

* [チュートリアル動画](https://www.youtube.com/watch?v=fWbM5DLh25U)ではAdministratorAccessポリシーを設定。もう少し減らす余地はないものか？
* アクティビティを確認できず、よく判らない。削除しても良さそう？

## Amazon Cognito ユーザープール

### amplify_backend_manager_*

* Amplify Admin UI に登録したユーザが並んでいる
* ユーザーを無効化すると、Webログオンセッションや、ローカルコンピュータ内 ~/.amplify/admin/config.json のトークンを無効化できる
  * ユーザーを再度有効化しても上記は戻らない
* 無効化したユーザーを有効化すると、Amplify Admin UI に再度ログインできるようになる
  * 開発者は amplify pull からやり直すことで復帰できる
