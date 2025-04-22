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
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=mern-application \
               -Dsonar.java.binaries=. \
               -Dsonar.projectKey=mern-application'''
               }
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
