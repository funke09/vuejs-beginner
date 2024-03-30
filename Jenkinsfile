pipeline {
    agent any
    
    stages {
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
                sh 'kubectl apply --validate=false -f deployment.yaml'
		sh 'kubectl apply --validate=false -f service.yaml'
            }
        }
    }
}

