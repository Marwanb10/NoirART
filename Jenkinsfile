pipeline {
  agent any
    stages {
      stage('Build') {
        steps {
          sh 'docker build -t maroine-noir-store:latest .'
        }
      }

      stage('Deploy') {
        steps {
          sh '(docker stop maroine-noir-store && docker rm maroine-noir-store) || true'
          sh 'docker run -d --restart unless-stopped -p 7002:80 --name maroine-noir-store maroine-noir-store:latest'
        }
      }
    }
}
