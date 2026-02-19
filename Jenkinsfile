pipeline {
  agent {
    kubernetes {
      inheritFrom 'kubectl-agent'
      defaultContainer 'kubectl'      
    }
  } 
  stage('Checkout') {
      steps {
        git 'https://github.com/madhuri75jha/k8s.git'
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
