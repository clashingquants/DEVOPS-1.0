pipeline {
    agent any
    environment {
        IMAGE_NAME = "devops-app"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/clashingquants/DEVOPS-1.0.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'eval $(minikube docker-env) && docker build -t $IMAGE_NAME:latest .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
                sh 'kubectl rollout restart deployment devops-app'
            }
        }
    }
}
