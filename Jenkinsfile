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
    stage('Running image') {
      agent any
      steps{
        script {
          sh ''' 
          docker run -it -p "project-jenkins:${BUILD_NUMBER}"
          curl 3.82.130.171:8000
          '''
          
        }
      }
    }
  }
}