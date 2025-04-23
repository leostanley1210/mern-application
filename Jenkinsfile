def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger'
    ]
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
      stage('codes analysis') {
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
    stage('docker push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                       sh 'docker tag mern-app-frontend leostanely1210/mern-app-frontend'
                       sh 'docker tag mern-app-backend leostanely1210/mern-app-backend'
                       sh 'docker push leostanely1210/mern-app-frontend'
                       sh 'docker push leostanely1210/mern-app-backend' 
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'slack Notification.'
            slackSend channel: '#jenkins',
            color: COLOR_MAP [currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URl}"
            
        }
    }
}   
