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
    stage('deploy front') {
     steps{

        withKubeConfig([credentialsId: 'mykubeconfig2', serverUrl: 'https://192.168.50.10:6443']) {
          sh 'kubectl apply -f kube/deployment/angular-deployment.yml --record'
          sh 'kubectl rollout restart deploy angular'

        }
        }
      }
    stage('deploy back') {
     steps{
        withKubeConfig([credentialsId: 'mykubeconfig2', serverUrl: 'https://192.168.50.10:6443']) {
          sh 'kubectl apply -f kube/deployment/node-deployment.yml --record'
          sh 'kubectl rollout restart deploy nodejs-deployment'

        }
      }
    }

  }
}
//  sudo docker build  -t  amin0894/back:46 .   usernem/repos


// docker push  amin0894/back:46
