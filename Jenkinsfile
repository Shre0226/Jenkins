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
        sh 'aws configure set aws_access_key_id ASIA4NVGMN52QWJIEWOM'
        sh 'aws configure set aws_secret_access_key aI8T45AK8dPR6jTDweXhi+LlImojJVWFqNP9HqTD'
        sh 'aws configure set default.region us-east-1'
        sh 'aws configure set default.output json'
        script {
          docker.withRegistry(
            'https://853973692277.dkr.ecr.us-east-1.amazonaws.com',
            'ecr:us-east-1:ec2-instance-credential') {
              def image = docker.build('shreya_jenkins_repo')

            }
          
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
       
     }
      
    }
  


   
  }
}
