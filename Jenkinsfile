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
          sh '''sudo docker build -t imagename . 
         '''
          sh '''sudo docker ps -a 
         '''
        
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
