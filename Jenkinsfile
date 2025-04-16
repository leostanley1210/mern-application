pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/leostanley1210/mern-application.git'
            }
        }
        stage('Run Docker Compose') {
            steps {
                script{
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
