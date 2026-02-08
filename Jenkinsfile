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
        sh '''
          set -e
          for i in $(seq 1 30); do
            if curl -fsS http://localhost:8085/health > /dev/null; then
              echo "Health OK"
              exit 0
            fi
            echo "Waiting for /health... ($i/30)"
            sleep 2
          done

          echo "Health check failed"
          docker compose ps || true
          docker compose logs --tail=80 nginx api || true
          exit 1
        '''
      }
    }
  }
}
