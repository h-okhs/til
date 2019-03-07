# JENKINS

## 仕組み

- ビルド結果  
  ビルド結果は Master の `${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}` に保存される。  
  成果物のアーカイブを指示しておけば、Slave 内の成果物を上記ディレクトリ内に Archive として保存できる。  
  またそれらは Jenkins のビルド結果画面から参照可能。

## プラグイン

- PowerShell プラグインで PowerShell コマンドを実行する場合は Master を WindowsContainer で動かさないと動かない  
  Bat コマンドから PowerShell なら可能

## パイプライン

- Pipeline で始めるのが Declarative Pipeline, node で始めるのが Scripted Pipeline

## 小ネタ

- コマンドプロンプトや PowerShell ウィンドウを立ち上げる場合は Start-Process を使う
- JENKINS_ROOT_URL/safeRestart で再起動指示画面に行ける
- sudo したいときは /etc/sudoers.d 配下にファイルを配置

## Docker jenkins

<https://github.com/jenkinsci/docker/blob/master/README.md>

- 起動
  docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
