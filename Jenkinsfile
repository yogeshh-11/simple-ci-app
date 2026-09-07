pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'deathangel11/simple-ci-app'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials-id'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yogeshh-11/simple-ci-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', "${REGISTRY_CREDENTIALS}") {
                        docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy stage - add deployment scripts here'
            }
        }
    }
}
