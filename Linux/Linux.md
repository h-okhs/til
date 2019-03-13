# Linux

## コマンドとか

- screen  
  長時間かかるコマンド実行などの場合に？開始してから Ctrl+a,d
  -ls -> -r(アタッチ)
- tar -zxvf
- CONFIGURE_OPTS="--disable-install-rdoc" rbenv install 2.2.4  
  ruby インストール
- jq  
  Json いじるツール

## vim

- Shift+v 範囲選択
- Ctrl+v 矩形選択
- d 削除
- y コピー
- p 貼り付け
- dd 1 行削除

## スクリプト

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

## 他

- リポジトリ  
  `$ sudo sed -i.bak -e "s%http://archive.ubuntu.com/ubuntu/%http://ftp.iij.ad.jp/pub/linux/ubuntu/archive/%g" /etc/apt/sources.list`
- 開発ツールインストール
  sudo apt-get install build-essenstial
- コンパイル時に lib が見つからないエラー
  共有ライブラリの探索パス追加

  ```sh
  mecab-config --libs-only-L | sudo tee /etc/ld.so.conf.d/mecab.conf
  sudo ldconfig
  ```
