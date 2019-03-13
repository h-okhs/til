# E2E テストの自動化環境構築

## 要件

- システムの E2E テストを自動化する
- テスト対象は Windows アプリ
- 動いてる様子を録画する

## 環境・使用ソフトウェア等

- 環境
  - Jenkins
  - AWS 上に Master Linux、 Slave Windows
  - ffmpeg で録画
  - テスト対象、テスト実行用アプリ、DB はリポジトリから持ってきてビルドする
  - テスト対象はサーバ Java・クライアント.Net で API 通信構成
  - DB サーバは Windows 上に構築
- ソフトウェア
  - Jenkins
  - Git
  - ffmpeg
  - FreeRDP
  - Xvfb
  - AutoHotKey
  - NuGet CLI
  - Visual Studio Community
  - Gradle

## Tech

- Job は Pipeline
- 録画するため Slave のデスクトップの描画が必要。録画しないなら一度リモートデスクトップを接続して切断しておけばよい。  
  描画するにはモニターにつながれているか、リモートデスクトップ接続で画面が表示されている必要あり。  
  ⇒ Master 上に Xvfb で仮想デスクトップを作成し、そこからリモートデスクトップ接続をして描画を維持。Job の最初に自動的に接続しに行く。  
  Xvfb はサービスとしてマシン起動時に実行。
- テスト対象のサーバと録画は終了を待てないため、PowerShell の Start-Process で非同期的に実行  
  ⇒ テスト終了後に終了させる必要がある。終了方法はプロンプトウィンドウに CTRL+C を送る必要あり。  
   ⇒ AutoHotKey でウィンドウをアクティブにして CTRL+C を送信する方式に。
- テスト対象のクライアントアプリはテスト実行用のアプリから起動されるためこちらも終了させる必要がある。  
  ⇒ Stop-Process で停止
- Slave 登録は Swarm プラグイン使用(Slave 側からの登録)。  
  リモデのログイン時に登録用スクリプトを走らせることで登録を Job 内で自動的に行われるようにしておく。
- .net のビルドは.NetCore でできるかと思ったが VisualStudio が必要だった。

## その他実施

- 構成の提案・すり合わせ
