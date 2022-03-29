pipeline {
  environment {
    imagename = "test-postmanlab"
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
          sh 'sudo docker build -t imagename . '
          sh 'sudo docker ps -a'
          sh 'sudo docker run -dp 8086:8086 --name postmanlb imagename'
          sh 'sudo docker tag postman gcr.io/maximal-run-343007/postmanlabs'
          sh 'sudo docker push gcr.io/maximal-run-343007/postmanlabs'
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
