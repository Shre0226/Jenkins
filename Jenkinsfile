pipeline {
  environment {
    registry = "Shre0226/Jenkins"
    registryCredential = 'github_creds'
    dockerImage = ''
  }
  agent any
  stages {
    
    stage('Building image') {
      agent {
                docker {
                    image 'docker'
                    // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
                    reuseNode true
                }
            }
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}