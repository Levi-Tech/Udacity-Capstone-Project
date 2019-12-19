pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e Blue-Green-Deployment/blue/*.html'
                sh 'tidy -q -e Blue-Green-Deployment/green/*.html'
 
            }
        }
        stage('Build and Publish Docker Image'){
                    steps {
                        sh 'docker build -t levi/blueimage -f Blue-Green-Deployment/blue/Dockerfile Blue-Green-Deployment/blue'
                        sh 'docker build -t levi/greenimage -f Blue-Green-Deployment/green/Dockerfile Blue-Green-Deployment/green'
                        sh 'docker push levi/blueimage'
                        sh 'docker push levi/greenimage'
                        sh 'docker rmi -f levi/greenimage'
                        sh 'docker rmi -f levi/blueimage'
                    }
                }
    }
}
