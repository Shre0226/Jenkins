pipeline {
  environment {
    registry = "Shre0226/Jenkins"
    registryCredential = 'github_creds'
    dockerImage = ''
  }
  agent any
  stages {

   
    
    stage('Building image') {
      agent any
      steps{
        script {
          dockerImage = docker.build "project-jenkins" + ":$BUILD_NUMBER"
          
        }
      }
    }
  }
}