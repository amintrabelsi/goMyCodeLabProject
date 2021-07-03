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
//   stage('Deploy front') {
//       steps {
//         script {
//           kubernetesDeploy(configs: "kube/deployment/angular-deployment.yaml", kubeconfigId: "mykubeconfig2")
//         }
//       }
//     }
//   stage('Deploy back') {
//       steps {
//         script {
//           kubernetesDeploy(configs: "kube/deployment/node-deployment.yaml", kubeconfigId: "mykubeconfig2")
//         }
//       }
//     }
//   }
  agent {
      kubernetes {
        	cloud 'kubernetes'
        	defaultContainer 'jnlp'
        }
      }
    stages {
      stage('Deploy App') {
        steps {
          script {
          kubernetesDeploy(configs: "kube/deployment/node-deployment.yaml", kubeconfigId: "mykubeconfig2")
          }
        }
      }
    }
}
//  sudo docker build  -t  amin0894/back:46 .   usernem/repos


// docker push  amin0894/back:46
