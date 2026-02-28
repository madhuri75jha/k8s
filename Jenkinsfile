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
            echo 'Application successfully deployed to Kubernetes!'
        }
        failure {
            echo 'Deployment failed. Check logs.'
        }
    }
}
