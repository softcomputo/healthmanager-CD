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

    stage('Erase previus deployment') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://2d655cb6-af0a-4dd2-9a34-6eba9635b23c.k8s.ondigitalocean.com --insecure-skip-tls-verify=true delete deployment hema '
          }

        }
      }
    stage('Deploy healthmanager') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://2d655cb6-af0a-4dd2-9a34-6eba9635b23c.k8s.ondigitalocean.com --insecure-skip-tls-verify=true apply -f hema-np.yaml '
          }

        }
      }

    }
  }
