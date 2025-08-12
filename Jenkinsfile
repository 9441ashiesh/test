pipeline {
  agent any

  environment {
    DEPLOY_DIR = "/var/www/html"
  }

  stages {
    stage('Checkout') {
      steps {
        // choose credentialsId matching how you set up creds
        git url: 'https://github.com/9441ashiesh/test.git', branch: 'main', credentialsId: 'github-https-creds'
      }
    }

    stage('Build (optional)') {
      steps {
        echo "If you have a build step (npm/yarn), add it here."
        // sh 'npm install && npm run build'
      }
    }

    stage('Deploy') {
      steps {
        echo "Copying files to ${DEPLOY_DIR}"
        sh """
          rm -rf ${DEPLOY_DIR}/* || true
          cp -r . ${DEPLOY_DIR}/
          chown -R www-data:www-data ${DEPLOY_DIR}
        """
      }
    }
  }

  post {
    success { echo "Deployed successfully" }
    failure { echo "Deployment failed" }
  }
}
