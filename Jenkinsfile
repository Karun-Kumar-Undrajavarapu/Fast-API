pipeline {
    agent any

    environment {
        IMAGE_NAME = "fastapi-app"
        CONTAINER_NAME = "fastapi-container"
        PORT = "8000"
    }

    stages {

        stage('Clone Code') {
            steps {
                echo "Code already present (Jenkins will clone automatically)"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d -p 8000:8000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }
}
