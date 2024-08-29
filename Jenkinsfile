pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE_PREFIX = "node"
        DOCKER_TAG = "v1.0"
    }
    
    tools {
        nodejs 'node'
    }

    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                script {
                    sh 'mv src/logo.svg src/old_logo.svg'
                    sh 'mv src/new_logo.svg src/logo.svg'
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
                    def imageName = env.BRANCH_NAME == 'main' ? 'nodemain' : 'nodedev'
                    docker.build("${imageName}:${DOCKER_TAG}")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def imageName = env.BRANCH_NAME == 'main' ? 'nodemain' : 'nodedev'
                    def port = env.BRANCH_NAME == 'main' ? '3000' : '3001' 

                    sh """
                        docker stop \$(docker ps -q --filter ancestor=${imageName}:${DOCKER_TAG}) || true
                        docker rm \$(docker ps -aq --filter ancestor=${imageName}:${DOCKER_TAG}) || true
                        docker run -d --expose ${port} -p ${port}:3000 ${imageName}:${DOCKER_TAG}
                    """
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'mv src/logo.svg src/new_logo.svg'
                sh 'mv src/old_logo.svg src/logo.svg'
            }
        }
    }
}
