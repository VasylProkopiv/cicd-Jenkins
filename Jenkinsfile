pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        script {
          echo 'This is a test stage'
          sh "docker stop AppFromDev"
          sh "docker rm AppFromDev"
          sh "docker rmi my-react-app"
          sh "docker build -t my-react-app ."
          sh "docker run -d -p 3000:3000 --name AppFromDev my-react-app"
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
