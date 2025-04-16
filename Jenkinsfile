pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/Sushmaa123/mern_application'
            }
        }
        stage('Run Docker Compose') {
            steps {
                script{
                    sh 'docker-compose up -d'
                }
            }
        }
    
    stage('docker push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'compose') {
                    sh 'docker push leostanely1210/mern'
                    }
                }
            }
        }
    }
}