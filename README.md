## 目的

GitHub の PullRequest に関する変更を Slack へ通知します。
通知タイミングは以下の通りです。

- PullRequest にレビュワーが追加された時
- PullRequest にレビュワーが Comment/Request Change/Approve を submit した時

## ローカル環境構築

homebrew で aws-sam-cli を追加します。
https://docs.aws.amazon.com/ja_jp/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html

```
$ brew tap aws/tap
$ brew install aws-sam-cli
```

## デバッグ方法

以下のコマンドでローカル API サーバを起動できます。

```
$ sam build --use-container
$ sam local start-api
```

エンドポイント向けに Postman 等で POST メソッドで json を投げることでテストできます。

## 新規メンバーの追加

SlackID をコピーして、MAP_USER_IDS に GitHubID と一緒に貼り付けてください

## ドキュメント

### GitHub から飛んでくる json

GitHub から飛んでくる json は events/を参考にしてください。

実際に飛んでくる JSON のパターンを試したい場合は[git-training](自分でテスト用のチャンネルを作ってください)で試せます。

Settings > Webhooks > 一覧の”Edit”ボタンをクリック > フッターに Webhooks から POST された内容が表示されます

### Slack API

https://api.slack.com/methods

### 環境変数

環境変数は Lambda に設定されているので、そこから持ってきてください。

ローカル環境では template.yml に追記することで渡すことができます
（GitHub で管理しないようにしたいので、コミットはしないでください。）

## デプロイ

template.yml と buildspec.yml を参考にしてください。

※ events の中身は下記のようで、ここには UP しません。

- approved.json
- change_request.json
- commented.json
- opened.json
- ready_for_review.json
- review_request.json

※ AWS の LICENSE も必要なので、ここには UP しません。
