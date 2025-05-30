pipeline {
  agent any
  tools {
    jdk "Java17"
    maven "Maven"
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
             // 8  // Creates a stage named 'SonarQube analysis'
    node {
      
      stage('SonarQube Analysis') {
        def mvn = tool 'Default Maven';
        withSonarQubeEnv() {
          sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Pilot-Proj -Dsonar.projectName='Pilot-Proj'"
        }
      }
    }                              

  }
}



