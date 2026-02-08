pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Up') {
      steps {
        sh '''
          set -e
          docker compose up -d --build
          docker compose ps
        '''
      }
    }

    stage('Health') {
      steps {
        sh 'curl -fsS http://localhost:8085/health'
      }
    }
  }
}
