pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/viveknshet96/flask_K8s_app3.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                eval $(minikube docker-env)
                docker build -t flask-k8s-app:1.0 .
                '''
            }
        }

        stage('Deploy to Kubernetes (Command Based)') {
            steps {
                sh '''
                kubectl delete deployment flask-k8s-deployment || true

                kubectl create deployment flask-k8s-deployment \
                  --image=flask-k8s-app:1.0

                kubectl expose deployment flask-k8s-deployment \
                  --type=NodePort \
                  --port=5000
                '''
            }
        }
    }
}
