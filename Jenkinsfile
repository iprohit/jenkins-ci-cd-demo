pipeline {
    agent {
        docker {
            image 'docker:20.10.16-dind' // Docker-in-Docker image
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

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
                sh 'docker version'
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
