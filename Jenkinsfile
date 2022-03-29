pipeline {
  environment {
    imagename = "test/postmanlabs"
    registryCredential = 'postman-dockerhub'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/priyankarag/test.git', branch: 'main', credentialsId: 'auth'])
 
      }
    }
    stage('Building image') {
      steps{
        script {
          sh 'sudo setfacl -m "g:docker:rw" /var/run/docker.sock'
          sh 'sudo addgroup --system docker'
          sh 'sudo adduser $USER docker'
          sh 'newgrp docker'
          sh 'docker build -t imagename .'
          sh 'docker ps -a'
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}
