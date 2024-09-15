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
          sh """
              if [ "\$(docker images -f 2>/dev/null)" = "true" ]; then 
              docker rmi nodedev:v1.0
              fi
          """
          sh "docker build -t nodedev:v1.0 ."
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          sh "docker run -d -p 3001:3001 --name $container_name nodedev:v1.0"
          sh "mv src/logo.svg src/dev.svg"
          sh "mv src/old_logo.svg src/logo.svg"
        }
      }
    }
  }
}
