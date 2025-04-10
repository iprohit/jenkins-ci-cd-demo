pipeline {
    agent any

    environment {
        DOCKER_USERNAME = credentials('dockerhub-creds')
        DOCKER_PASSWORD = credentials('dockerhub-creds')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t rodocker10/nodejs-app .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                sh 'docker push rodocker10/nodejs-app'
            }
        }
    }
}
