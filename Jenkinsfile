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
          sh 'gcloud auth configure-docker'
          sh 'sudo docker tag imagename gcr.io/maximal-run-343007/postmanlabs'
          sh 'sudo docker push gcr.io/maximal-run-343007/postmanlabs'
      }
    }

    stage('Remove Unused docker image') {
      steps{
        sh 'sudo docker rmi $imagename:$BUILD_NUMBER'
         sh 'sudo docker rmi $imagename:latest'

      }
    }
  }
}
