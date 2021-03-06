# grpc

## 概要

- サービス間の情報のやり取りを行う通信技術の一つ
  
  マイクロサービス間でも利用されている

- 元はgoogleが開発したRPC技術がベース(stubby)

- 通信に使用するプロトコル(トランスポート)にデフォルトではHTTP/2、データのシリアライズにProtocol Buffersを使用する

- 類似の技術にXML-RPC、HTTP/HTTPSベースのJSON-RPC等が存在する

## gPRCを使用するメリット

- クライアント・サーバー間でのデータフォーマットを定義(サービス定義ファイル)を作成し、クライアント・サーバーそれぞれのコードを自動的に生成を行う事が可能

- 概ねの言語に対応しており、前述したサービス定義ファイルからそれぞれの言語のコードを出力する事が可能である。

  クライアント・サーバーでそれぞれ異なる言語でもやり取りを調整する必要がない

## gPRCのデメリット

- デバッグ(通信周り)がやりづらいらしい

- Node.js、Go等でのやり取りはそこまで恐らく難しいものではないが、クライアント側がWebとなると制約が生じる

  ブラウザの実装としてgPRCを解釈する事が出来ない為、サーバーとの間にプロキシーを置く必要がある(envoy)

## プロキシーが必要な理由

参考:

https://yuku.takahashi.coffee/blog/2019/01/grpc-proxy-for-grpc-web

## Protocol Buffers

- 型付けされたデータや構造化されたデータをネットワーク経由にてやり取り出来るフォーマットに変換する為の技術

- 構造化されたデータをバイト列に変換する処理をシリアライズ等と呼ぶ

- JSONやXMLと異なる点は、データ構造の型を定義する点にある

  JSONでもシリアライズすれば他の言語で解釈する事は可能であるが、その際にデータの型情報が無い為、厳密に解釈させるにはある程度クライアント・サーバで調整が必要となる

### プロトコル定義ファイル

- データ構造やサービスを定義したファイル

- 拡張子は、「.proto」

- 現在(2020/10/15)バージョンはバージョン2とバージョン3が存在する

  特に理由がない場合はバージョン3を使用する

- 以下のようにファイル中にてバージョンを明示する

```
syntax="proto3";
```

#### メッセージ

- Protocol Buffersでやり取りするデータを指す

```
message <定義するメッセージ型の名前> {
    <型> <フィールド名1>=<フィールド番号>;
    :
    :
}
```

- 定義する型名はCamelCase(単語の先頭一文字を大文字)

- フィールド名はsnake_case(単語はすべて小文字、_区切り)

- フィールド番号は各フィールド毎に一意な1～536,870,911までの整数を指定。連続している必要はない

  あとからフィールド名や型を変更してもフィールド番号が一致していれば同じものとして認識される

- フィールド番号はシリアル化された際に1～15までが1バイト、16～2047までが2バイトにエンコードされるので頻繁に利用するデータは1～15の番号を使用する事が推奨される

- 下記に記載された型以外にも定義したメッセージを型にする事、メッセージ型の定義中にさらに別のメッセージを定義する入れ子構造も可能。

```
message Account {
    unit32 id=1;
    string password=2;
}

message User {
    string name=1;
    Account accout=2;
    message icon {
        unit32 width=1;
        unit32 height=2;
        string path=3;
    }
}
```

- 型

|型名|説明|制約|デフォルト値|
|:-|:-|:-|:-|
|double|倍精度浮動小数点数(64ビット)||0|
|float|単精度浮動小数点数(32ビット)||0|
|int32|符号あり32ビット整数||0|
|int64|符号あり64ビット整数||0|
|unit32|符号なし32ビット整数||0|
|unit64|符号なし64ビット整数||0|
|sint32|符号あり32ビット整数|int32よりも負数を効率的にエンコード可能|0|
|sint64|符号あり64ビット整数|int64よりも負数を効率的にエンコード可能|0|
|fixed32|符号なし32ビット整数(固定バイト幅)||0|
|fixed64|符号なし64ビット整数(固定バイト幅)||0|
|sfixed32|符号あり32ビット整数(固定バイト幅)|int32よりも大きい値を効率的にエンコード可能|0|
|sfixed64|符号あり64ビット整数(固定バイト幅)|int64よりも大きい値を効率的にエンコード可能|0|
|bool|ブール型(true/false)||false|
|string|UTF-8もしくは7ビットASCII文字列|4,294,967,296バイトまで|空文字列|
|bytes|バイト列|4,294,967,296バイトまで|空バイト列|

※デフォルト値は値が定義されていない場合に設定される

[言語別の型マッピング](https://developers.google.com/protocol-buffers/docs/proto3#scalar)

#### 列挙型

```
enum <定義する列挙型名> {
    <フィールド1>=<フィールド番号>;
    :
    :
}
```

#### oneof

複数の型のいずれかを持つフィールドを定義する際に使用する

```
message ProcessResult {
    oneof result {
        Process process=1;
        Error error=2;
    }
}
```

#### map

ハッシュ型

```
map <<キー名の型>, <値の型>> <フィールド名>=<フィールド番号>;
```

#### コメント

```
//1行のコメント

/*
 1行目のコメント
 2行目のコメント
 */
```

#### インポート

```
import "<ファイルパス>";

import public "<ファイルパス>";
```

- 通常は、インポートされたファイル内の定義のみが参照可能

- import publicを使用するとインポートされたファイル内のさらにインポートされたファイルも参照する事が可能になる

#### パッケージ

- 名前空間

- 「.」(ピリオド)により階層構造も可能

```
package <パッケージ名>
```

他のパッケージから参照する場合は、「パッケージ名.メッセージ名」となる

#### reserved

将来の拡張の為にフィールド番号を予約済みにする事

```
message <メッセージ名> {
    reserved <フィールド番号1>, <フィールド番号2>, ...
}
```

#### サービス

```
service <サービス名> {
  rpc <プロシージャー名> (<引数として受け取るメッセージ型>) returns (<戻り値として返すメッセージ型>) {}
  :
  :
}
```

### コード生成

- プロトコル定義ファイルより各言語向けのクラスファイルを生成するには「protoc」を使用する

- node.jsの場合は、「grpc-tools」パッケージを使用する(内部でprotocが使用される)

[サンプル](https://github.com/use200371/proto-sample)

## RPC方式

クライアント:サーバー

|方式|説明|用途
|:-|:-|:-|
|Unary RPCs|1 リクエスト、1 レスポンス|シンプルな実装|
|Server streaming RPCs|1 リクエスト、多レスポンス|クライアントからのリクエストは必要なので厳密にはサーバープッシュとは異なるが、複数のレスポンスを返す事が可能|
|Client streaming RPCs|多リクエスト、1 レスポンス||
|Bidirectional streaming RPCs|多リクエスト、多レスポンス|双方向ストリーミング|


https://github.com/3p3r/grpc-express