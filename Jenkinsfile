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
          sh 'sudo docker build -t postmanlab . '
          sh 'sudo docker ps -a'
          sh 'sudo docker run -dp 8085:8086 --name postmanlab postmanlab'
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
