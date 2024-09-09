pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        script {
          container_name = "AppFromDev"
          sh "if [ "$( docker container inspect -f '{{.State.Running}}' AppFromDev 2>/dev/null )" = "true" ]; then docker stop $container_name; fi"
          sh "docker build -t my-react-app ."
          sh "docker run -d -p 3000:3000 --name $container_name my-react-app"
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
