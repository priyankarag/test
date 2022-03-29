pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                    ENV LC_ALL=C.UTF-8
                    ENV LANG=C.UTF-8

                    RUN apt update -y && apt install python3-pip git -y && pip3 install --no-cache-dir pipenv

                    ADD Pipfile Pipfile.lock /httpbin/
                    WORKDIR /httpbin
                    RUN /bin/bash -c "pip3 install --no-cache-dir -r <(pipenv lock -r)"

                ADD . /httpbin
                RUN pip3 install --no-cache-dir /httpbin
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
