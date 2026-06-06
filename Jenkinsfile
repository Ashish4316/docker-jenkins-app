pipeline {

    agent any

    environment {
        IMAGE_NAME = "docker-jenkins-app"
        GIT_AUTH = credentials('github-creds')
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run --rm %IMAGE_NAME%'
            }
        }

        stage('Login to ghcr Hub') {
            steps {
                bat 'echo %GIT_AUTH_PSW% | docker login ghcr.io -u %GIT_AUTH_USR% --password-stdin'
            }
        }

        stage('Tag image for ghcr') {
            steps {
                bat 'docker tag %IMAGE_NAME% ghcr.io/Ashish4316/%IMAGE_NAME%:v1'
            }
        }

        stage('Push Image to ghcr'){
            steps {
                bat 'docker push ghcr.io/Ashish4316/%IMAGE_NAME%:v1'
            }
        }
    }
}