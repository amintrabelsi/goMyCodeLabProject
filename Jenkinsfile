pipeline {
    environment {
    registryfront = "amin0894/front"
    registryback = "amin0894/back"
dockerImage =''
    registryCredential = 'dockerhub_id'
  }
  agent any
  stages {
    stage('Building front image') {
      steps{
        script {

        dockerImage=  docker.build (registryfront + ":$BUILD_NUMBER" , "./angular-app")
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
         dockerImage = docker.build (registryback + ":$BUILD_NUMBER" ,"./express-server")
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