### Amazon EBSについて
**参考**
https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/ebs-volume-types.html

**ボリュームについて**
- EBSボリュームのパフォーマンスに影響を与える要因
  - インスタンス構成
  - I/O特性
  - ワークロードのデマンド
  - など。。。
- プロビジョニングされたIOPSを最大限活用するためにはEBS最適化インスタンスを利用する。

**IOPSクレジットについて**
- ボリュームのサイズに応じて、ボリュームに割り当てられるIOPSクレジットが決まる。
- 時間の経過に応じて、IOPSクレジットが回復する。
- IOPSクレジットが0になると、ボリュームのパフォーマンスが低下する。
