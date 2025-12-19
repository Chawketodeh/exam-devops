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
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f ci-cd-config/k8s-serveur-deployment.yaml'
                sh 'kubectl apply -f ci-cd-config/k8s-client-deployment.yaml'
            }
        }
    }
}
