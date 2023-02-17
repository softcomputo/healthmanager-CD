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
    stage('Erase healthmanager') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'token-k8s-do', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://1ba7c9fd-b9dc-4a43-9ce2-66a2ce9aec8b.k8s.ondigitalocean.com --insecure-skip-tls-verify=true delete deployment healthmanager '
          }

        }
      }
    stage('clean images') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'token-k8s-do', variable: 'api_token')
                      ]) {
            sh 'docker system prune --force'
          }

        }
      }
    stage('Deploy healthmanager') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'token-k8s-do', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://1ba7c9fd-b9dc-4a43-9ce2-66a2ce9aec8b.k8s.ondigitalocean.com --insecure-skip-tls-verify=true apply -f hm_deployment.yaml '
          }

        }
      }
    stage('Deploy svc healthmanager') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'token-k8s-do', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://1ba7c9fd-b9dc-4a43-9ce2-66a2ce9aec8b.k8s.ondigitalocean.com --insecure-skip-tls-verify=true apply -f hema-svc.yaml '
          }

        }
      }

    }
  }
