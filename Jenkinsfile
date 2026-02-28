pipeline {
  agent {
    kubernetes {
      inheritFrom 'kubectl-agent'
      defaultContainer 'kubectl'
    }
  }
  stages {
    stage('Deploy to Kubernetes') {
      steps {
        sh '''
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
        '''
      }
    }
    stage('Verify Deployment') {
      steps {
        sh '''
        kubectl get pods
        kubectl get svc
        '''
      }
    }
  }
  post {
    success {
      echo 'Application SUCCESSFULLY deployed to KUBERNETES!!!'
    }
    failure {
      echo 'Deploment FAILED!!!!!', check LOGS.'
    }
  }
}
