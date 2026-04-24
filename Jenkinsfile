pipeline {
    agent any

    environment {
        IMAGE_NAME = "varun124477/myapp"
    }

    stages {

        stage('Clone Source') {
            steps {
                git 'https://github.com/varun124477/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh '''
                    echo $DOCKER_TOKEN | docker login -u varun124477 --password-stdin
                    '''
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}