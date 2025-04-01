pipeline {
    agent any

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
                withCredentials([usernamePassword(credentialsId: '7c910bc4-e2e4-48a4-857c-51be93277e96', usernameVariable: 'rohith1305', passwordVariable: 'Rohith@1305')]) {
                    sh 'echo  | docker login -u  --password-stdin'
                    sh 'docker push rohith1305/ecommerce-backend:latest'
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
