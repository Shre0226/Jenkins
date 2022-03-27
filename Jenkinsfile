pipeline {
  environment {
    registry = "Shre0226/Jenkins"
    registryCredential = 'github_creds'
    dockerImage = ''
  }
  agent any
  stages {

   
    
    stage('Building image') {
     
      steps{
        script {
          dockerImage = docker.build "project-jenkins" + ":$BUILD_NUMBER"
          
        }
      }
    }
    stage('Running image') {
     
      steps{
        script {
          sh ''' 
          docker run -d -p 8000:8000 "project-jenkins:${BUILD_NUMBER}"
          '''
          
        }
      }
    }

    stage('Deploy image in production EC2') {
  
      steps{
        sshagent(credentials: ['AWSSecretKey']) {
        sh 'ssh -o StrictHostKeyChecking=no ec2-user@54.197.9.239 ls'
        }
      }
    }
  }
}
