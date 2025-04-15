pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/leostanley1210/Chat_Room.git'
            }
        }

        stage('docker build') {
            steps {
                script {
                sh 'docker build -t leostanely1210/chatroom .'
              }
           }
        }

        stage('docker push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                    sh 'docker push leostanely1210/chatroom'
                    }
                }
            }
        }
       stage('docker container'){
           steps {
               script {
                   sh 'docker run -itd --name chatroom-cont -p 8081:8080 leostanely1210/chatroom'
                }
            }
        }
     }
 }