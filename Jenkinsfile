pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-login') // Jenkins credential ID
        IMAGE_NAME = "shaikvasim/flask-app"  // Replace with your exact repo name
        IMAGE_TAG = "latest"                    // Or use a fixed tag
    }
    stages {
        stage('Docker Login & Pull Image') {
            steps {
                bat """
                    docker login -u %DOCKERHUB_CREDENTIALS_USR% -p %DOCKERHUB_CREDENTIALS_PSW%
                    docker pull %IMAGE_NAME%:%IMAGE_TAG%
                """
            }
        }
        stage('Stop Old Container') {
            steps {
                bat 'docker rm -f flask_app || exit 0'
            }
        }
        stage('Run New Container') {
            steps {
                bat """
                    docker run -d ^
                    --name flask_app ^
                    -p 5000:5000 ^
                    %IMAGE_NAME%:%IMAGE_TAG%
                """
            }
        }
    }
}