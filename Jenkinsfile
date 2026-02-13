pipeline {
    agent any

    tools {
        jdk 'JAVA17'
        maven 'MAVEN3'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Reshufowzi/java-webapp-jenkins.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build & Deploy') {
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
