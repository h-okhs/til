# JENKINS

## Docker jenkins

<https://github.com/jenkinsci/docker/blob/master/README.md>

- 起動
  docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts

- Powershell コマンドを実行したい場合は WindowsContainer で動かさないと動かない
