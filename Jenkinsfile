pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://your-repo-url.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t your-dockerhub-username/ecommerce-backend:latest backend/'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo  | docker login -u  --password-stdin'
                    sh 'docker push your-dockerhub-username/ecommerce-backend:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 your-dockerhub-username/ecommerce-backend:latest'
            }
        }
    }
}
