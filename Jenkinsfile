
pipeline {
  agent any

  environment {
        CONTAINER_NAME = "AppFromMain"
  }
  
  stages {
    stage("build") {
      steps {
        script {
          sh "mv src/logo.svg src/old_logo.svg"
          sh "mv src/prod.svg src/logo.svg"
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
          sh "docker build -t nodemain:v1.0 ."
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          sh "docker run -d -p 3000:3000 --name $container_name nodemain:v1.0"
          sh "mv src/logo.svg src/prod.svg"
          sh "mv src/old_logo.svg src/logo.svg"
        }
      }
    }
  }
}
