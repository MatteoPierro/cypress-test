pipeline {
  agent any

  stages {
    stage ('Checkout') {
        steps {
            checkout scm
        }
    }

    stage ('Test') {
      steps {
        dir("e2e") {
          script {
            ansiColor('xterm') {  
                sh 'mkdir results'
                sh 'docker-compose up --build --abort-on-container-exit'
            }
          }
        }
      }
      post {
          always {
              junit 'results/*.xml'
              sh 'docker-compose down'
              sh 'docker system prune -af'
          }
      }
    }
  }
}
