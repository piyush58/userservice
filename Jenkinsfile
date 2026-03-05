pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    environment {
        DOCKER_USER = "piyushkumar11"
        IMAGE_NAME = "userservice"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/piyush58/userservice.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_USER/$IMAGE_NAME:1.0 .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_USER/$IMAGE_NAME:1.0'
            }
        }

        stage('Deploy') {
            steps {
                sh 'helm upgrade --install userservice helm/userservice'
            }
        }
    }
}