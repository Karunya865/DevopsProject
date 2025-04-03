pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "karunya08/devopsproject"
        K8S_DEPLOYMENT = "devopsproject-deployment"
        K8S_NAMESPACE = "default"
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:latest ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh "docker push ${DOCKER_IMAGE}:latest"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig([credentialsId: 'k8s-cluster-credentials']) {
                    sh "kubectl apply -f k8s/deployment.yaml"
                    sh "kubectl rollout status deployment/${K8S_DEPLOYMENT} -n ${K8S_NAMESPACE}"
                }
            }
        }
    }

    post {
        failure {
            echo 'Build or Deployment Failed'
        }
        success {
            echo 'Deployment Successful'
        }
    }
}
