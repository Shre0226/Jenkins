pipeline {
  environment {
    registry = "Shre0226/Jenkins"
    registryCredential = 'github_creds'
    dockerImage = ''
  }
  agent any
  stages {

    stage('Cloning Git') {
      steps {
        git url: 'https://github.com/Shre0226/Jenkins.git'
        sh "ls -lat"
      }
    }
    
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