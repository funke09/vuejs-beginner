pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: '54eb5b5f-b607-4b9f-88b1-011260c6419c', url: 'https://github.com/funke09/vuejs-beginner.git'
            }
        }
        
        stage('Dockerize') {
            steps {
                sh 'docker build -t vuejs-ci-cd .'
            }
        }
        
        stage('Push to Registry') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
		    sh "docker tag vuejs-ci-cd:latest funke09/vuejs-ci-cd:latest"
                    sh 'docker push funke09/vuejs-ci-cd:latest'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}

