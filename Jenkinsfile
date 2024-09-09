pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        script {
          container_name = AppFromDev
          echo 'This is a test stage'
          #sh "if [ "$( docker container inspect -f '{{.State.Running}}' AppFromDev 2>/dev/null )" = "true" ]; then docker stop $container_name; fi"
          
          sh "docker stop AppFromDev
              docker rm AppFromDev
              docker rmi my-react-app
              docker build -t my-react-app .
              docker run -d -p 3000:3000 --name AppFromDev my-react-app"
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
