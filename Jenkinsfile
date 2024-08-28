pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS 7.8.0'
    }
    
    environment {
        DOCKER_IMAGE = "myapp"
        DOCKER_TAG = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Prepare Logo') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        sh 'cp logos/main-logo.svg public/logo.svg'
                    } else if (env.BRANCH_NAME == 'dev') {
                        sh 'cp logos/dev-logo.svg public/logo.svg'
                    }
                }
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    def port = env.BRANCH_NAME == 'main' ? 3000 : 3001
                    
                    // Зупиняємо і видаляємо попередній контейнер, якщо він існує
                    sh "docker stop ${DOCKER_IMAGE}-${env.BRANCH_NAME} || true"
                    sh "docker rm ${DOCKER_IMAGE}-${env.BRANCH_NAME} || true"
                    
                    // Запускаємо новий контейнер
                    docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").run("-d --name ${DOCKER_IMAGE}-${env.BRANCH_NAME} -p ${port}:3000")
                    
                    echo "Application deployed on http://localhost:${port}"
                }
            }
        }
    }
    
    post {
        success {
            echo "Pipeline успішно завершено! Застосунок доступний на http://localhost:${env.BRANCH_NAME == 'main' ? 3000 : 3001}"
        }
        failure {
            echo 'Pipeline завершився з помилкою.'
        }
    }
}
