pipeline {
    agent any
  stages {
     stage('Build') {
        steps {   
           sh 'cd /home/vagrant/rialto-cicd/secondary-audit-service && sudo ./gradlew -Pprod bootWar jibDockerBuild --image=secondaryauditservice --no-daemon'
          }
        }
     stage('get-login-aws') {     
       steps {
        sh 'sudo aws ecr get-login-password --region us-east-1 | sudo docker login --username AWS --password-stdin 592473443790.dkr.ecr.us-east-1.amazonaws.com'
        }
     }    
     stage('tag and push') {    
       steps {
        sh 'TAG=DEV2.1.${BUILD_NUMBER}'  
        sh 'sudo docker tag secondaryauditservice:latest 592473443790.dkr.ecr.us-east-1.amazonaws.com/service/secondary-audit-service:latest'
        sh 'sudo docker tag secondaryauditservice:latest 592473443790.dkr.ecr.us-east-1.amazonaws.com/service/secondary-audit-service:TAG'
        sh 'sudo docker push 592473443790.dkr.ecr.us-east-1.amazonaws.com/service/secondary-audit-service:latest'
        sh 'sudo docker push 592473443790.dkr.ecr.us-east-1.amazonaws.com/service/secondary-audit-service:TAG'
            }
        }
    }
}
