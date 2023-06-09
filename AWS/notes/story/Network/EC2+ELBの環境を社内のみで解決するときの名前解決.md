## EC2+ELBのアプリを社内のみで利用するときの名前解決について
---
**ストーリー：**
社内のみアクセスできるアプリケーションをAWSへ移行する。
名前解決には社内のクライアントPCのホストファイルを利用していた。

アプリケーションはEC2にホストし、その前段にELBを配置する。
名前解決の方法として最適なものは何か？
**解決策：**
Route53のプライベートなリソースレコードとしてEC2のホスト名を設定する。
Aliasレコードを利用してELBの名前を設定する。
**理由：**
ELBがスケーリングする際にIPアドレスが変わるため、ホストファイルに記載すると都度更新が必要になる。
そのため、ELBの名前を設定して名前解決する必要がある。
また、今回は社内用のアプリケーションで社内からのアクセスのため、Route53のプライベートなリソースレコードを利用する。
