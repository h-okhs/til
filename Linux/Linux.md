# Linux

## コマンドとか

- screen  
  長時間かかるコマンド実行などの場合に？開始してから Ctrl+a,d
  -ls -> -r(アタッチ)
  スクロール
- tar
  - -zxvf
  - -zx
- CONFIGURE_OPTS="--disable-install-rdoc" rbenv install 2.2.4  
  ruby インストール
- jq  
  Json いじるツール
- curl
  - -X GET HTTP メソッド指定
  - -u USER:PASSWORD
  - -H "Content-Type:application/json"
  - -d {"id":"aaa", "text":"東京" } データ指定
  - --data-binary @filename (ファイル内容送信)
- xargs
  - 標準出力を引数にコマンド実行 echo a b c d | xargs -I{} basename {}
  - -t コマンド表示
  - -n 引数として使う入力の個数
- sed
  - 正規表現置換したうえで標準出力できる
  - デリミタわりと自由
- rpm
  - -ivh インストール
- シンボリックリンク
  - 実体コピー cp -L symlink copied
  - 実体をアーカイブ tar h オプション
- rename
  - rename perl 正規表現 対象ファイル
  - rename s/.csv/.tsv/ \*.csv

## Shell スクリプト

- trap
  最後に必ず実行するコマンドを記述
  trap "rm /tmp/..." 0
- if

  ```
    if [ $aa -eq 0 ] ; then
        echo aa
    elif
        ...
    else
        ...
    fi
  ```

- ディレクトリ存在チェック  
  if [ -d "$DIRECTORY" ] ; then
- not
  - if [ ! $aa = "aa" ] ; then
- $!で直前実行のプロセスのPID取得　$?で終了ステータス

## vim

- Shift+v 範囲選択
- Ctrl+v 矩形選択
- d 削除
- y コピー
- p 貼り付け
- dd 1 行削除

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

## 仮想デスクトップ

```
Xvfb :1 -screen 0 1920x1080x24
export DISPLAY=:1
```

```
xvfb-run --server-num=1 [デスクトップアプリ起動コマンド]
```

## 他

- リポジトリ変更
  ```
  sudo sed -i.bak -e "s%http://archive.ubuntu.com/ubuntu/%http://ftp.iij.ad.jp/pub/linux/ubuntu/archive/%g" /etc/apt/sources.list
  ```
- 開発ツールインストール
  ```
  sudo apt-get install build-essenstial
  ```
- コンパイル時に lib が見つからないエラー
  共有ライブラリの探索パス追加

  ```sh
  mecab-config --libs-only-L | sudo tee /etc/ld.so.conf.d/mecab.conf
  sudo ldconfig
  ```

- SSH の鍵と config は自分オーナー 600 にする
