pipeline {
    environment {
    registryfront = "amin0894/front"
    registryback = "amin0894/back"

    registryCredential = 'dockerhub_id'
  }
  agent any
  stages {
    stage('Building front image') {
      steps{
        script {

          docker.build (registryfront + ":$BUILD_NUMBER" , ./angular-app)
        }
      }

    }
     // Uploading Docker images into Docker Hub
    stage('Upload  front Image') {
     steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }


stage('Building back image') {
      steps{
        script {
          docker.build (registryback + ":$BUILD_NUMBER" ,./express-server)
        }
      }

    }
     // Uploading Docker images into Docker Hub
    stage('Upload  back Image') {
     steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }


  }
}