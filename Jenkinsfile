pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-flask-app"
        DOCKERHUB_USER = credentials('dockerhub-username')
        DOCKERHUB_PASS = credentials('dockerhub-password')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/YourUser/YourRepo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh "echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin"
                    sh "docker tag $IMAGE_NAME $DOCKERHUB_USER/$IMAGE_NAME:latest"
                    sh "docker push $DOCKERHUB_USER/$IMAGE_NAME:latest"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh "docker run -d -p 5000:5000 --name flask_app $DOCKERHUB_USER/$IMAGE_NAME:latest"
                }
            }
        }
    }
}