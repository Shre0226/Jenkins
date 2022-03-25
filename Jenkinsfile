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
          sh ''' yum install docker-engine -y
                service docker start
              '''
          
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
          
        }
      }
    }
  }
}