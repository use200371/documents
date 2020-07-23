# Node.js

## Node.jsインストール

複数のNode.jsのバージョン管理を見越した上でバージョン管理ツールの「nodist」をインストールする

下記のURLよりインストーラーをダウンロードし、インストールを行う

[nodist](https://github.com/nullivex/nodist)

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