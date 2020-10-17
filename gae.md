# GAE

## VPCネットワーク

- RFC1918(プライベートネットワーク)

  要するにローカルネットワークのアドレス範囲

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

## Cloud Sql

### プライベートIP

- プライベートIPを使用する事でパブリックIPと比較してネットワークレイテンシーが低くなる

- 他のサービス(GCEやGAE等)から接続するには、VPCネットワークのサーバーレスVPCアクセスを使用する必要がある(最小でGCEのマイクロインスタンス程度の課金額が発生する)

### 接続不可

- Cloud Shellからの接続、インスタンス名指定での接続は行えない。

- RFC1918(プライベートネットワーク)に接続できるネットワーク以外は接続出来ない。

- 安全かつ簡単に接続するには、「パブリックIP+Cloud Proxy Sql」を使用する。

### データベース作成

- コンソールからは照合文字列?が「en_US.UTF-8」のデータベースしか作成できないので注意

  (並び順なんか気にしなければ問題ないが)

- Cloud Sqlへ接続して作成する以外は今のところ調整は出来ない

  下記のコマンドのようにgcloudコマンドでも行えない(template0が指定出来ない為)

```
gcloud sql databases create [DATABASE_NAME] --instance=[INSTANCE_NAME] [--charset=CHARSET] [--collation=COLLATION]

例. gcloud sql databases create test-db --instance=test-instance --charset=ja_JP.UTF8 --collation=

```

https://cloud.google.com/sql/docs/postgres/external-connection-methods?_ga=2.41750372.-772748756.1547894084
https://cloud.google.com/sql/docs/postgres/sql-proxy
https://cloud.google.com/sql/docs/postgres/private-ip?hl=ja
https://cloud.google.com/sql/docs/postgres/authorize-networks?hl=ja
https://cloud.google.com/vpc/docs/configure-serverless-vpc-access?hl=ja
https://cloud.google.com/sdk/gcloud/reference/sql/connect?hl=ja

- App Engine から Cloud SQL への接続
https://cloud.google.com/sql/docs/postgres/connect-app-engine?hl=ja

- サーバーレス VPC アクセスの構成
https://cloud.google.com/vpc/docs/configure-serverless-vpc-access?hl=ja



https://qiita.com/AK_qloud/items/2f6903a25b4ee132346b

GAE/Go + Cloud Build でデプロイを自動化しよう
https://qiita.com/wezardnet/items/6175cc09ede9b7f79f79