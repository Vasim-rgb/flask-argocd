pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-username')
        IMAGE_NAME = "vasimshaik/flask-argocd"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}:latest"
                }
            }
        }
    }
}