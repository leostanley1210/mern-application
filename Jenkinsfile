pipeline {
   agent any
    environment {
     SCANNER_HOME = tool 'sonar-scanner'
    }
   stages {
      stage('git checkout') {
        steps {
            git 'https://github.com/leostanley1210/mern-application.git'  
        }
      }
      stage('code analysis') {
        steps {
            withSonarQubeEnv('sonar-server') {
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Chat_Room \
               -Dsonar.java.binaries=. \
               -Dsonar.projectKey=mern-application'''
               }
        }
      }
      stage('docker build') {
        steps {
            script {
              sh 'docker build -t mern-application .' 
            }
      }
    }
   stage('docker container') {
         steps {
            script {
               sh 'docker run -itd --name chat-room -p 8082:8080 mern-application'
              }
          }
    }    
 }       
}