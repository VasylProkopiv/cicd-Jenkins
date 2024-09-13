pipeline {
  agent any

  environment {
        CONTAINER_NAME = "AppFromDev"
  }
  
  stages {
    stage("build") {
      steps {
        script {
          sh "mv src/logo.svg src/old_logo.svg"
          sh "mv src/dev.svg src/logo.svg"
        }
      }
    }
    stage("test") {
      steps {
        script {
          sh """
              if [ "\$(docker container inspect -f '{{.State.Running}}' ${env.CONTAINER_NAME} 2>/dev/null)" = "true" ]; then 
                  docker stop ${env.CONTAINER_NAME}
                  docker rm ${env.CONTAINER_NAME}
              fi
          """
        }
      }
    }
    stage("build docker image") {
      steps {
        script {
          sh "docker build -t my-react-app ."
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          sh "docker run -d -p 3000:3000 --name $container_name my-react-app"
          sh "mv src/logo.svg src/dev.svg"
          sh "mv src/old_logo.svg src/logo.svg"
        }
      }
    }
  }
}
