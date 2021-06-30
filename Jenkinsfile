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

        dockerImage=  docker.build (registryfront , "./angular-app")
        }
      }

    }
     // Uploading Docker images into Docker Hub
    stage('push front Image') {
     steps{
         script {
            docker.withRegistry( '', registryCredential ) {
           dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
            }
        }
      }
    }


stage('Building back image') {
      steps{
        script {
         dockerImage = docker.build (registryback ,"./express-server")
        }
      }

    }
     // Uploading Docker images into Docker Hub
    stage('push  back Image') {
     steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
            }
        }
      }
    }


  }
}

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config