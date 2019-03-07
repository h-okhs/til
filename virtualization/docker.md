# Docker

## コマンド

### docker run

- ポートマッピング  
  -p [ホスト側ポート]:[コンテナ側ポート]
- バックグラウンド実行  
  -d
- コンテナ削除後実行  
  -rm
- ボリュームをマウント
  -v(standalone), --mount(swarm)

## ボリューム

指定したパスのディレクトリをコンテナ内ではなくホスト側に生成する。

## タイムゾーン

Java のオプションを指定 & -v でタイムゾーンファイルをアタッチする
docker run -d -v jenkins_home:/var/jenkins_home -v /usr/share/zoneinfo/Tokyo:/usr/localtime -e JAVA_OPTS="-Duser.timezone=Asia/Tokyo" -p 80:8080 -p 60000:60000 jenkins/jenkins:lts