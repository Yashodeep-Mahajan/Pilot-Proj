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
      // stage('SonarQube Analysis') {
      //   steps {
      //       withSonarQubeEnv('SonarQube') {
      //           sh 'sonar-scanner -Dsonar.projectKey=your_key -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=$SONAR_TOKEN'
      //             }
      //         }                           

  }
}



