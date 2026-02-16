pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ varshini400/java-webapps-jenkins.git'
            }
        }

        stage('Build with Maven (Docker)') {
            steps {
                sh '''
                  docker run --rm \
                    -v "$PWD":/app \
                    -w /app \
                    maven:3.9.9-eclipse-temurin-21 \
                    mvn clean package
                '''
            }
        }

        stage('Docker Build & Run') {
            steps {
                sh '''
                  docker stop java-webapp || true
                  docker rm java-webapp || true

                  docker build -t java-webapp:1.0 .
                  docker run -d -p 8081:8081 --name java-webapp java-webapp:1.0
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Java Web Application deployed successfully'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}

