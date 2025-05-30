pipeline {
  agent any
  tools {
    jdk "Java17"
    maven "Maven"
    sonarQube 'SonarQube'
  }
  stages{
    stage ("Cleanup Workspace"){
      steps{
        cleanWs()
        }
     }
    stage ("Checkout from SCM"){
      steps{
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/Yashodeep-Mahajan/Pilot-Proj.git'
        }
     }
      stage ("Build Application"){
        steps{
            sh "mvn clean package"    
        }
     }
      stage ("Test Application"){
        steps{
            sh "mvn test"    
         }
     }
     node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Pilot-Proj -Dsonar.projectName='Pilot-Proj'"
    }
  }
}
  }
}



