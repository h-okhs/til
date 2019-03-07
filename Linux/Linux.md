# Linux

## Shell

- $!で直前実行のプロセスのPID取得　$?で終了ステータス

## タイムゾーン変更

ディストリビューションによって違うので注意
ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

- Amazon Linux
  /etc/sysconfig/clock を編集

## 自前サービス登録

Redhat7 からは systemctl に変わったそう

```
## 動かすサービスを作る
$ sudo vim /usr/local/bin/hello_world.sh
$ cat /usr/local/bin/hello_world.sh
#!/bin/sh

while :
do
    echo "Hello, World. (PID=$(echo $$), DATE=$(date))"
    sleep 30
done

## ユニット定義ファイルを作る
$ sudo vim /etc/systemd/system/hello_world.service
$ cat /etc/systemd/system/hello_world.service
[Unit]
Description=hello_world
After=network.service

[Service]
Type=simple
Restart=on-success
ExecStart=/usr/local/bin/hello_world.sh

[Install]
WantedBy=multi-user.target

## 起動
$ sudo systemctl start hello_world

## 自動起動の設定
$ sudo systemctl enable hello_world
```
