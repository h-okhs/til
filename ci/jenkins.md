# JENKINS

## 仕組み

- ビルド結果  
  ビルド結果は Master の ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/\${BUILD_NUMBER} に保存される。  
  成果物のアーカイブを実行することで、Slave 内の成果物を上記ディレクトリ内に Archive として保存できる。  
  またそれらは Jenkins のビルド結果画面から参照可能。

## Docker jenkins

<https://github.com/jenkinsci/docker/blob/master/README.md>

- 起動
  docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts

- Powershell コマンドを実行したい場合は WindowsContainer で動かさないと動かない  
  Bat コマンドから PowerShell なら可能？
