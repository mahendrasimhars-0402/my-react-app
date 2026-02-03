pipeline {
    agent any

    environment {
        IMAGE_NAME = 'mahendrasimha0403/my-react-app'
        DOCKERHUB_CREDENTIALS = 'dockerhub'
    }

    stages {

        stage('Checkout code') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:mahendrasimhars-0402/my-react-app.git',
                    credentialsId: 'github-ssh-key'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline build successfully!"
        }
        failure {
            echo "Pipeline build Failed!"
        }
    }
}
