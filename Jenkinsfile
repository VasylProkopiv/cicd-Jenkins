pipeline {
    agent any
    tools {
        nodejs 'NodeJS 7.8.0'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
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
                    def imageName = env.BRANCH_NAME == 'main' ? 'nodemain' : 'nodedev'
                    sh "docker build -t ${imageName}:v1.0 ."
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def imageName = env.BRANCH_NAME == 'main' ? 'nodemain' : 'nodedev'
                    def port = env.BRANCH_NAME == 'main' ? '3000' : '3001'
                    
                    sh """
                        docker stop \$(docker ps -q --filter ancestor=${imageName}:v1.0) || true
                        docker rm \$(docker ps -aq --filter ancestor=${imageName}:v1.0) || true
                        docker run -d --expose ${port} -p ${port}:3000 ${imageName}:v1.0
                    """
                }
            }
        }
    }
}
