pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                // Build Docker image
                sh 'docker build -t vuejscicd:v1 .'
            }
        }
        stage('Push to Registry') {
            steps {
                // Push Docker image to registry
                sh 'docker push vuejscicd:v1'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                // Apply Kubernetes manifest files
                sh 'kubectl apply -f deployment.yaml -f service.yaml'
            }
        }
    }
}

