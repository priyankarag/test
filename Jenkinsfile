pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                echo 'Building..'
                gcloud auth configure-docker
                docker build -t testpostman .
                docker ps -a
                echo 'build'
                }
            }
     
        }
        stage('Test') {
            steps {
                echo 'Testing. python.'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
