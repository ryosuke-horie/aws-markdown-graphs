### AWSサービス（EC2,S3,DynamoDb）へのVPCエンドポイント導入
---
**ストーリー：**
SaaSサービスのセキュリティの向上を求め、設定を変更する。
現状のサービスでは複数リージョンで運用されていて、複数のEC2をELBで負荷分散している。
EC2インスタンスは起動時にクレデンシャル情報をS3から取得する。
データストアにはDynamoDBを利用している。

セキュリティ向上のため、以下を検討する。
- データの信頼性を高めたい
- EC2インスタンスからのAWSサービスへのアクセスをインターネット経由からインターナルネットワーク経由に変更したい。

**解決策：**
VPCエンドポイントを利用して、EC2からS3,DynamoDBへのアクセスをインターネット経由からインターナルネットワーク経由に変更する。
以下の追加設定が必要になる。
- EC2からのアクセスをインターナルネットワーク経由に変更するため、S3とDynamoDB用のゲートウェイエンドポイントを作成する。
- S3に保存されたEC2の起動設定をバックアップするためにS3のクロスリージョンレプリケーションを有効にする。
- DynamoDBのグローバルテーブルを有効にする。

**理由：**
S3とDynamoDBはリージョナルサービスである。信頼性を高めるには、別リージョンにバックアップを取る必要がある。
また、EC2からのアクセスは通常、ネットワーク経由のAPIで行われる。
VPCエンドポイントを利用することでAWSのデータセンター内のインターナルネットワーク経由でのAPIアクセスが可能になる。
そのためにはS3とDynamoDB用にVPCエンドポイントのゲートウェイエンドポイントを有効化する必要がある。