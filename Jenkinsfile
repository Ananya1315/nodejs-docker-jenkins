pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t nodejs-api .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker stop nodejs-api-container || exit 0'
                bat 'docker rm nodejs-api-container || exit 0'
                bat 'docker run -d -p 3000:3000 --name nodejs-api-container nodejs-api'
            }
        }

        stage('Test API') {
            steps {
                bat 'curl http://localhost:3000/status'
            }
        }
    }
}