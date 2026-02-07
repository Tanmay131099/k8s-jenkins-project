pipeline {
  agent any

  stages {
    stage('Show files') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        container('kubectl') {
          sh 'kubectl version --client'
          sh 'kubectl apply -f deployment.yaml'
          sh 'kubectl apply -f service.yaml'
        }
      }
    }
  }
}

