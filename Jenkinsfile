pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        sh '''java -version
mvn --version
git --version'''
      }
    }
    stage('Deploy healthmanager') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'eks-token', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://BA4AB3262CEF109B9D355F2C0ABE06AF.gr7.us-east-1.eks.amazonaws.com --insecure-skip-tls-verify=true apply -f hm_deployment.yaml '
          }

        }
      }

    }
  }
