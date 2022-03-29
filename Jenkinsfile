pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                echo 'Building..'
                docker build -t testpostman .
                docker ps -a
           
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
