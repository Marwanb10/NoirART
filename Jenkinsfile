pipeline {
  agent any
    stages {
      stage('Build') {
        when {
          expression { env.BRANCH_NAME in ['prod'] }
        }

        steps {
          sh 'docker build -t maroine-noir-store:latest .'
        }
      }

      stage('Deploy') {
        when {
          expression { env.BRANCH_NAME in ['prod'] }
        }

        steps {
          sh '(docker stop maroine-noir-store && docker rm maroine-noir-store) || true'
          sh 'docker run -d --restart unless-stopped -p 7001:80 --name maroine-noir-store maroine-noir-store:latest'
        }
      }
    }
}
