pipeline {
    agent any
    tools {
        nodejs 'node'
    }
    stages {
        stage('Diagnostics') {
            steps {
                sh 'node --version'
                sh 'npm --version'
                sh 'which node'
                sh 'which npm'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
    }
}
