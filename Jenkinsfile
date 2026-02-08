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
        sh '/var/jenkins_home/bin/kubectl version --client'
        sh '/var/jenkins_home/bin/kubectl apply -f deployment.yaml'
        sh '/var/jenkins_home/bin/kubectl apply -f service.yaml'
      }
    }
  }
}
