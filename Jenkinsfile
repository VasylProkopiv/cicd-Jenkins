pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        script {
          echo 'This is a test stage'
          sh "docker build -t my-react-app ."
          sh "docker run -d -p 3000:3000 my-react-app"
        }
      }
    }
    stage("test") {
      steps {
        echo 'This is a test stage'
      }
    }
    stage("build docker image") {
      steps {
        echo 'This is a test stage'
      }
    }
    stage("deploy") {
      steps {
        echo 'This is a deploy stage'
      }
    }
  }
}
