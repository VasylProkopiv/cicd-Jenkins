pipeline {
  agent any
  stages {
    stage("checkout") {
      steps {
        echo 'This is a checkout stage'
      }
    }
    stage("build") {
      steps {
        echo 'This is a test stage'
        sh "docker build -t my-react-app ."
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
        sh "docker run -p 3000:3000 my-react-app"
      }
    }
    stage("deploy") {
      steps {
        echo 'This is a deploy stage'
      }
    }
  }
}
