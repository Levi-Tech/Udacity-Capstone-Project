pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e Blue-Green-Deployment/blue/*.html'
                sh 'tidy -q -e Blue-Green-Deployment/green/*.html'
               
            }
        }
        stage('creates a Docker container'){
                    steps {
                        sh 'docker build -t  levitech/blueimage -f Blue-Green-Deployment/blue/Dockerfile Blue-Green-Deployment/blue'
                        sh 'docker build -t  levitech/greenimage -f Blue-Green-Deployment/green/Dockerfile Blue-Green-Deployment/green'
                        sh 'docker push  levitech/blueimage'
                        sh 'docker push  levitech/greenimage'
                        sh 'docker rmi -f  levitech/greenimage'
                        sh 'docker rmi -f  levitech/blueimage'
                    }
                }
        stage('blue/green deployment'){
            steps {
                sh 'kubectl apply -f ./blue-controller.json'
                sh 'kubectl apply -f ./green-controller.json'
                sh 'kubectl apply -f ./blue-green-service.json'
            }
        }    
            
    }
}
