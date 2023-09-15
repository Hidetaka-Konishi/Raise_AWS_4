# VPCの作成方法
1. AWSのマネジメントコンソールのVPCから「VPCを作成」をクリックする。
2. 以下のようにVPCを識別しやすくするために名前をつける。

![スクリーンショット 2023-09-15 135031](https://github.com/Hidetaka-Konishi/Raise_AWS_4/assets/142459457/59d1e015-a7fd-4f8b-b56d-fcf403560239)

3. 一番下までスクロールして「VPCを作成」をクリックする。
# 

# sshでEC2に接続する方法
コマンドプロンプトで```ssh -i "~/Downloads/```を入力するが実行はまだしない。AWSのマネジメントコンソールで接続したいEC2から「接続」をクリックし、「SSHクライアント」タブをクリックすると 例：```ssh -i "KrrXp2bKjU3chCVq.pem" ec2-user@ec2-44-212-7-64.compute-1.amazonaws.com``` と記載されているので```KrrXp2bKjU3chCVq.pem" ec2-user@ec2-44-212-7-64.compute-1.amazonaws.com```の部分だけコピーし、さっき入力した```ssh -i "~/Downloads/```とつなげた状態である```ssh -i "~/Downloads/KrrXp2bKjU3chCVq.pem" ec2-user@ec2-44-212-7-64.compute-1.amazonaws.com```を実行する。
