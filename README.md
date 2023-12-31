※セキュリティグループはインバウンドで絞って、アウトバウンドは全開にする。

# VPCの作成
1. AWSのマネジメントコンソールのVPCから「VPCを作成」をクリックする。
2. 「名前タグの自動生成」では、VPCを識別しやすくするために名前をつける。
3. 一番下までスクロールして「VPCを作成」をクリックする。

# EC2の作成
1. AWSのマネジメントコンソールのEC2から「インスタンスを起動」をクリックする。
2. インスタンスに名前をつける。
3. 「アプリケーションおよび OS イメージ (Amazon マシンイメージ)」の項目では、Amazon Linux 2 AMIを選択する。
4. 「キーペア」の項目の「キーペア名」では、既存のキーペアを選択もしくは新たに作成する。
5. 「ネットワークの設定」の項目では、EC2をデプロイしたいと思っているVPCとAZを選択する。「パブリック IP の自動割り当て」で「有効化」を選択する。「インバウンドセキュリティグループのルール」では通信を許可したいポートやIPアドレスの範囲を指定する。ちなみに、「ソースタイプ」で「自分のIP」を選択すると自分のPCからのみ通信を許可するという設定になる。
6. 「高度な詳細」の項目では、「DNS ホスト名」で「リソースベースの IPv4 (A レコード) DNS リクエストを有効化」にチェックを入れる。「キャパシティーの予約」は「開く」を選択する。
7. 最後に、画面右にある「インスタンスを起動」をクリックする。

# RDSの作成
1.  AWSのマネジメントコンソールのRDSから「データベースの作成」をクリックする。
2. 「エンジンのオプション」の項目で、データベースを選択する。
3. 「テンプレート」の項目では、開発する規模を考えて選択する。今回は学習用なので「無料利用枠」を選択する。
4. 「設定」の項目の「DB インスタンス識別子」で識別しやすい名前をつける。「マスターパスワード」で任意のパスワードを入力し、メモしておく。
5.  「ストレージ」の項目で、今回は学習用なので「ストレージの自動スケーリング」の「ストレージの自動スケーリングを有効にする」のチェックは外しておく。
6. 「接続」の項目では、「VPC」でRDSをデプロイしたいVPCを選択する。「既存の VPC セキュリティグループ」でセキュリティグループ名を選択するとそのセキュリティグループからのみ通信を許可するという設定になる。「アベイラビリティーゾーン」ではRDSと接続したいと思っているインスタンスがあるAZを選択する。
7. 「追加設定」の項目では、「ログのエクスポート」のチェックリストにすべてチェックをいれておく。
8.  画面を一番下までスクロールして「データベースの作成」をクリックする。

# SSHでEC2に接続
Powershellで```ssh -i "~/Downloads/```を入力するが実行はまだしない。AWSのマネジメントコンソールで接続したいEC2から「接続」をクリックし、「SSHクライアント」タブをクリックすると 例：```ssh -i "KrrXp2bKjU3chCVq.pem" ec2-user@ec2-44-212-7-64.compute-1.amazonaws.com``` と記載されているので```KrrXp2bKjU3chCVq.pem" ec2-user@ec2-44-212-7-64.compute-1.amazonaws.com```の部分だけコピーし、さっき入力した```ssh -i "~/Downloads/```とつなげた状態である```ssh -i "~/Downloads/KrrXp2bKjU3chCVq.pem" ec2-user@ec2-44-212-7-64.compute-1.amazonaws.com```を実行する。

# EC2からRDSに接続
1. PowerShellを開き、上記の「sshでEC2に接続」の手順に沿ってEC2に接続する。
2. 接続するRDSがMySQLで、EC2インスタンスにMySQLがインストールされていない場合は、```sudo yum install mysql```を実行してインストールを行う。
3. ```mysql -h [RDSのエンドポイント] -P 3306 -u [RDSのユーザー名(デフォルトはadmin)] -p```を実行する。
4. パスワードが求められるのでRDSインスタンスを作成するときに設定したパスワードを入力することで以下のように接続していることを確認できる。

![](./image/mysql_connect.png)
