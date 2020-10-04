# grpc

## 概要



## プロキシーが必要な理由

参考:

https://yuku.takahashi.coffee/blog/2019/01/grpc-proxy-for-grpc-web

## RPC方式

クライアント:サーバー

|方式|説明|用途
|:-|:-|:-|
|Unary RPCs|1 リクエスト、1 レスポンス|シンプルな実装|
|Server streaming RPCs|1 リクエスト、多レスポンス|サーバープッシュ|
|Client streaming RPCs|多リクエスト、1 レスポンス||
|Bidirectional streaming RPCs|多リクエスト、多レスポンス|双方向ストリーミング|