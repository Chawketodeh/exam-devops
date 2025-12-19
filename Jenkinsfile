pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Server') {
            steps {
                sh 'docker build -t serveur:latest serveur'
            }
        }
        stage('Build Client') {
            steps {
                sh 'docker build -t client:latest client'
            }
        }
        stage('Load images to Minikube') {
            steps {
                sh '''
                    minikube image load serveur:latest
                    minikube image load client:latest
                '''
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply --validate=false -f ci-cd-config/k8s-serveur-deployment.yaml
                    kubectl apply -f ci-cd-config/k8s-client-deployment.yaml
                '''
            }
        }
    }
}
