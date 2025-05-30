pipeline {
  agent any

  tools {
    jdk "Java17"
    maven "Maven"
  }

  environment {
    APP_NAME = "register-app-pipeline"
    RELEASE = "1.0.0"
    DOCKER_USER = "monkeymindaroundworld"
    DOCKER_PASS = 'Docker'
    IMAGE_NAME = "${DOCKER_USER}/${APP_NAME}"
    IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
  }

  stages {
    stage("Cleanup Workspace") {
      steps {
        cleanWs()
      }
    }

    stage("Checkout from SCM") {
      steps {
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/Yashodeep-Mahajan/Pilot-Proj.git'
      }
    }

    stage("Build Application") {
      steps {
        sh "mvn clean package"
      }
    }

    stage("Test Application") {
      steps {
        sh "mvn test"
      }
    }

    stage("Build & Push Docker Image") {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
    sh """
      echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
      docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
      docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest
      docker push ${IMAGE_NAME}:${IMAGE_TAG}
      docker push ${IMAGE_NAME}:latest
    """

          }
        }
      }
    }
  }
}



// pipeline {
//   agent any
//   tools {
//     jdk "Java17"
//     maven "Maven"
//     // sonarQube 'SonarQube'
//   }
//    // environment {
//   	// APP_NAME = "register-app-pipeline"
//    //      RELEASE = "1.0.0"
//    //      DOCKER_USER = "monkeymindaroundworld"
//    //      DOCKER_PASS = 'Docker'
//    //      IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
//    //      IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
//    //  }
  
//   stages{
//     stage ("Cleanup Workspace"){
//       steps{
//         cleanWs()
//         }
//      }
//     stage ("Checkout from SCM"){
//       steps{
//         git branch: 'main', credentialsId: 'github', url: 'https://github.com/Yashodeep-Mahajan/Pilot-Proj.git'
//         }
//      }
//     stage ("Build Application"){
//         steps{
//             sh "mvn clean package"    
//         }
//      }
//     stage ("Test Application"){
//         steps{
//             sh "mvn test"    
//          }
//      }
//       // stage("Build & Push Docker Image") {
//       //       steps {
//       //           script {
//       //               docker.withRegistry('',DOCKER_PASS) {
//       //                   docker_image = docker.build "${IMAGE_NAME}"
//       //               }

//       //               docker.withRegistry('',DOCKER_PASS) {
//       //                   docker_image.push("${IMAGE_TAG}")
//       //                   docker_image.push('latest')
//       //               }
//       //           }
//       //       }

//        }
    
//     }
// }



