pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                echo 'Building..'
                docker build -t testpostman .
                docker ps -a
                docker run testpostman -p 8084:8084 -d
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
