# GIT

## アンチパターン

<https://speakerdeck.com/lemiorhan/10-git-anti-patterns-you-should-be-aware-of>

- コミットごとにプッシュする
  - コミットを修正する機会を失う
-

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

### 長いパスを扱えるようにする

git config --system core.longpaths true

## コマンド

- 元に戻す
  - コミット後
    - 履歴は残してコミットはやめにする
      - git revert [commit] 指定したコミットを取り消すコミットを作成
    - コミットだけやめる(追加修正してコミットやり直したいなど)
      - git reset --soft HEAD^
    - コミット・ステージをやめる
      - git reset --mixed HEAD^
  - ステージ後・ステージをやめる
    - git reset --mixed HEAD
  - コミット・ステージ・ローカル全部やめる
    - git reset --hard HEAD^
  - ステージング前
    - git checkout [filename]
- 直前のコミットを変更
  - コミットコメント修正  
    git commit --amend -m "message"
  - 追加コミット
    git commit --amend -m "message"  
    git commit --amend --no-edit
- タグをチェックアウト  
  git checkout refs/tags/[tagname]
- ブランチをチェックアウト
  git checkout [branchname]

## プルリク

## レビュー・マージ
