# GAE

## Cloud Sql

- データベース作成

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