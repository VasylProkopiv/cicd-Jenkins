pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        script {
          container_name = AppFromDev
          sh '''
              docker stop AppFromDev || true
              docker rm AppFromDev || true
              docker rmi my-react-app || true
              docker build -t my-react-app .
              docker run -d -p 3000:3000 --name AppFromDev my-react-app
          '''
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
