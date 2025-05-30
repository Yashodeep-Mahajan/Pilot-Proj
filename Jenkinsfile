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
      stage('SonarQube analysis') {         // 8  // Creates a stage named 'SonarQube analysis'
              environment {                     // 9  // Defines environment variables specific to this stage
                  scannerHome = tool 'SonarQube'  
                                                // Sets the SonarQube scanner tool
              }                                 // 9  // Ends the environment block for this stage
  
              steps {                           // 10  // Defines the steps that will be executed in this stage
                  withSonarQubeEnv('SonarQube') {  
                                                // Executes the SonarQube analysis within the SonarQube environment
                      sh "${scannerHome}/bin/sonar-scanner"  
                                                // Runs the SonarQube scanner tool
                  }                             // Ends the withSonarQubeEnv block
              }                                 // 10  // Ends the steps block for 'SonarQube analysis' stage
          }                                     // 8  // Ends the 'SonarQube analysis' stage

  }
}



