pipeline {
  agent {label "linux"}
  options {
    buildDiscarder logRotator(artifactDaysTokeepStr: '', artifactNumTokeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
    disableConcurrentBuilds()
  }
  stages {
    stage('Hello') {
      steps { 
        echo "hello"
      }
    }
  }
}

