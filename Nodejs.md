# Node.js

## 対象環境

- Windows 10

## Node.jsインストール

インストーラーをnode.jsの[公式サイト](https://nodejs.org/ja/)からダウンロードし、インストールを行う事も出来る

リリースは偶数バージョンが長期サポート(LTS)の対象となる

現状では約3年でおおよそサポートが終了するサイクルでリリースされています

新しいバージョンがリリース毎に再インストールするのは色々な手間が生じます。

そこでNode.jsのバージョン管理ツールの「nodist」を使用し、node.jsをインストールする

[nodist](https://github.com/nullivex/nodist)のインストーラーをダウンロードし、インストールを行う

- 利用可能なバージョン一覧

```
nodist dist
```

- 指定バージョンをインストール

```
nodist + [バージョン]
または
nodist [バージョン] <-インストールと選択

例.
nodist 12.18.1
```

- インストールされているバージョン確認

```
nodist list
```

- 指定バージョンに切り替え
  
```
nodist [バージョン]

例.
nodist 12.18.1
```

## npx

npxはローカルモジュールの呼び出しが可能になるコマンド

ただ、nodistでインストールした場合に付属しない為、別途インストールする必要がある

```
npm i -g npx
```

使用方法

```
npx [モジュール名]
```

## typescript

```
npm install -D typescript @types/node
```

### tsconfig.jsonの作成

```
npx tsc --init
```

### express

```
npm install -D @types/express
```

## cloud build

「APIとサービス」より「App Engine Admin API」を有効にする

「IAMと管理」にて「xxxxxxxxxx@cloudbuild.gserviceaccount.com」へ以下のロールを割り当てます。

- App Engine デプロイ担当者

- App Engine サービス管理者

- Cloud Build サービス アカウント

Cloud Tasksを使用する場合は以下のロールを割り当てます。

- Cloud Scheduler 管理者

- クラウドタスク管理者

- Cloud Tasks サービス エージェント

サーバーレス VPC アクセス ユーザー

