pipeline {
  agent any

  environment {
        CONTAINER_NAME = "AppFromDev"
  }
  
  stages {
    stage("build") {
      steps {
        script {
          sh """
              if [ "\$(docker container inspect -f '{{.State.Running}}' ${env.CONTAINER_NAME} 2>/dev/null)" = "true" ]; then 
                  docker stop ${env.CONTAINER_NAME}
                  docker rm ${env.CONTAINER_NAME}
              fi
          """
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
