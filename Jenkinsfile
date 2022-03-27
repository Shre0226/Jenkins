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
          docker run -d -p 8000:8000 "project-jenkins:${BUILD_NUMBER}"
          '''
          
        }
      }
    }

    stage('Deploy image in production EC2') {
      agent any
      steps{
        sshagent(credentials: ['AWSSecretKey']) {
        sh 'ssh ec2-user@54.197.9.239 ls'
        }
      }
    }
  }
}
