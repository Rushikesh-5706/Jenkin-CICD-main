pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                  docker build -t maven-web-app .
                '''
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                  docker stop webapp || true
                  docker rm webapp || true

                  docker run -d \
                    --name webapp \
                    -p 8081:8080 \
                    maven-web-app
                '''
            }
        }
    }
}
