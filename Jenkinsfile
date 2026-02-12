pipeline {
  agent any

  stages {

    stage('Build (Validate manifests)') {
      steps {
        sh 'echo "Validating Kubernetes YAML..."'
        sh '/var/jenkins_home/bin/kubectl apply --dry-run=client -f deployment.yaml'
        sh '/var/jenkins_home/bin/kubectl apply --dry-run=client -f service.yaml'
      }
    }

    stage('Deploy') {
      steps {
        sh '/var/jenkins_home/bin/kubectl apply -f deployment.yaml'
        sh '/var/jenkins_home/bin/kubectl apply -f service.yaml'
      }
    }

    stage('Test (Smoke test nginx)') {
      steps {
        sh '''
          echo "Testing nginx from inside the cluster..."
          /var/jenkins_home/bin/kubectl run curl-test --rm -i --restart=Never \
            --image=curlimages/curl:8.5.0 \
            -- curl -sS http://my-nginx-service.default.svc.cluster.local | head -n 5
        '''
      }
    }
  }
}
