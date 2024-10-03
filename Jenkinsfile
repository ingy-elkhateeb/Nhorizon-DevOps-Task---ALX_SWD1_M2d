pipeline {
    agent any 

    environment {
        DOCKER_CREDENTIALS = 'dockerhub-credentials' // Jenkins credentials ID for Docker Hub
        DOCKER_IMAGE = 'ingyelkhateeb/nhorizon-java-container:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/XP2600-hub/nhorizon-java-container.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                    
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
    }
   
}