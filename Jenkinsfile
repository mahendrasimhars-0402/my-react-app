pipeline {

    agent any

    environment {
        IMAGE_NAME = "mahendrasimha0403/my-react-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'git@github.com:mahendrasimhars-0402/my-react-app.git'
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

        stage('Push To Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline Success "
        }
        failure {
            echo "Pipeline Failed "
        }
    }
}
