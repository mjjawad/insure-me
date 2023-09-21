pipeline{
 agent any
 tools {
  maven 'M2_HOME'
     }
stages{
  stage('Git Checkout') {
  steps {
  git 'https://github.com/mjjawad/insure-me.git'
        }
     }
  stage('Build Package'){
    steps {
           sh 'mvn package'
          }
       }  
   stage('Publish Html Reports'){
      steps {
           publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/insureme-project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])       
            }
         }
   stage('Create Docker Image Of App'){
      steps{
           sh 'docker build -t jawadjk786/insure-me-app:1.0 .'
           }
        }  
   stage('Docker image push'){
      steps{
            withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
           sh 'docker login -u jawadjk786 -p ${dockerHubPwd}'
            }
           sh 'docker push jawadjk786/insure-me-app:1.0 .'
       
           }
    
        }
    } 
}
