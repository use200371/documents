# Node.js

## 対象環境

- Windows 10

## 概要

- リリースは偶数バージョンが長期サポート(LTS)の対象となる

  現状では約3年でおおよそサポートが終了するサイクルでリリースされています

## Node.jsインストール

- インストーラーをnode.jsの[公式サイト](https://nodejs.org/ja/)からダウンロードし、インストールを行う事も出来る

  ただ、新しいバージョンのリリース毎、プロジェクトの指定毎に再インストールするのは色々な手間が生じます。

- そこでNode.jsのバージョン管理ツールの「nodist」を使用し、node.jsをインストールする

  [nodist](https://github.com/nullivex/nodist)のインストーラーをダウンロードし、インストールを行う

  (Macの場合は、「nodebrew」「nvm」、他には「nodeenv」「anyenv」も存在する)

### nodist

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

- npxはローカルモジュールの呼び出しが可能になるコマンド

  (やっている事はnode_modules/bin/配下を呼び出している)

- ただ、nodistでインストールした場合に付属しない為、下記のコマンドにて別途インストールする必要がある

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



