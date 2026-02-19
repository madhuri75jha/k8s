pipeline {
  agent {
    kubernetes {
      inheritFrom 'kubectl-agent'
      defaultcontainer 'kubectl'      
    }
  } 
  stages {
    stage('Deploy to Kubernetes') {
      steps {
        sh '''
        kubectl apply -f k8s/deployment.yaml
        kubectl apply -f k8s/service.yaml
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
      echo 'Application successfully DEPLOYED in KUBERNETES!'
    }
    failure {
      echo 'Deployment failed.Check LOGS.'
    }
  }
}
