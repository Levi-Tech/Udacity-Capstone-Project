pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e blue-green/blue/*.html'
                sh 'tidy -q -e blue-green/green/*.html'
                sh 'hadolint blue-green/blue/Dockerfile'
                sh 'hadolint blue-green/green/Dockerfile'
            }
        }
        stage('Build and Publish Docker Image'){
                    steps {
                        sh 'docker build -t levitech/blueimage -f blue-green/blue/Dockerfile blue-green/blue'
                        sh 'docker build -t levitech/greenimage -f blue-green/green/Dockerfile blue-green/green'
                        sh 'docker push levitech/blueimage'
                        sh 'docker push levitech/greenimage'
                        sh 'docker rmi -f levitech/greenimage'
                        sh 'docker rmi -f levitech/blueimage'
                    }
                }
    }
}
