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
          aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 853973692277.dkr.ecr.us-east-1.amazonaws.com
          docker push "project-jenkins:${BUILD_NUMBER}"
          '''
          
        }
      }
    }

    stage('Deploy image in production EC2') {
  
    
      steps{
        sshagent(credentials: ['AWSSecretKey']) {
        sh 'ssh -o StrictHostKeyChecking=no ec2-user@54.197.9.239 aws ecr get-login --no-include-email --region us-east-1'
        sh 'ssh -o StrictHostKeyChecking=no ec2-user@54.197.9.239 docker pull 853973692277.dkr.ecr.us-east-1.amazonaws.com/shreya_jenkins_repo:latest'
        sh 'ssh -o StrictHostKeyChecking=no ec2-user@54.197.9.239 docker run -d -p 8000:8000 853973692277.dkr.ecr.us-east-1.amazonaws.com/shreya_jenkins_repo:latest'
        sh 'ssh -o StrictHostKeyChecking=no ec2-user@54.197.9.239 curl localhost:8000'
        }
        ec2-instance-role
     }
      }
    }
  


   
  }
}
