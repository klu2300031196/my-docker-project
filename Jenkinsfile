pipeline {
    agent any

    environment {
        IMAGE_NAME = "ghcr.io/klu2300031196/my-docker-project"
        TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/klu2300031196/my-docker-project.git',
                    branch: 'main',
                    credentialsId: 'github-credentials'
                )
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%TAG% ."
            }
        }

        stage('Login to GHCR') {
            steps {
                withCredentials([string(credentialsId: 'github-token', variable: 'TOKEN')]) {
                    bat "echo %TOKEN% | docker login ghcr.io -u klu2300031196 --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push %IMAGE_NAME%:%TAG%"
            }
        }
    }
}