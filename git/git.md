# GIT

## Windows 用 初期設定

### SSH 鍵を独自のファイル名にし、パスフレーズの入力を省略する

1. 鍵を作成  
   `$ ssh-keygen -b 2048 -t rsa -f github_id_rsa -C "mail@mail.com"`
2. SSH エージェントを起動  
   OpenSSH Authentication Agent サービスを起動
3. エージェントに鍵を追加  
   `$ ssh-add github_id_rsa`
4. .ssh/config を作成

   ```.ssh/config
   Host github-xxx
    HostName github.com
    IdentityFile ~/.ssh/github_id_rsa
    TCPKeepAlive yes
    IdentitiesOnly yes
    User git
   ```

5. Git の SSH を OpenSSH にする  
   環境変数 GIT_SSH = c:\WINDOWS\System32\OpenSSH\ssh.exe
6. 接続テスト

   ```shell
   ssh -T github-xxx
   git fetch
   ```
