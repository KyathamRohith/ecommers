pipeline {
    agent any
       environment {
    DOCKER_CREDENTIALS = '7c910bc4-e2e4-48a4-857c-51be93277e96'
       }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/KyathamRohith/ecommers.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t rohith1305/ecommerce-backend:latest backend/'
            }
        }

       stage('Push to Docker Hub') {
    steps {
        script {
            withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                // Login securely using --password-stdin
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'

                    sh 'docker push rohith1305/ecommerce-backend:latest'
                }
            }
        }
       }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 rohith1305/ecommerce-backend:latest'
            }
        }
    }
}
