pipeline {
    agent any

    environment {
        IMAGE_NAME = 'karunya865/devopsproject'
        CONTAINER_REGISTRY = 'docker.io'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Karunya865/DevopsProject.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push $IMAGE_NAME:latest'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
