pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                sh 'kubectl apply --dry-run=client -f k8s/'
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }

        stage('Verify') {
            steps {
                sh 'kubectl rollout status deployment/cicd-web -n cicd-lab'
                sh 'kubectl get pods -n cicd-lab'
                sh 'kubectl get service -n cicd-lab'
            }
        }
    }
}
