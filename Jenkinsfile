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
                        sh 'docker build -t levitech/blueimage -f Blue-Green-Deployment/blue/Dockerfile Blue-Green-Deployment/blue'
                        sh 'docker build -t levitech/greenimage -f Blue-Green-Deployment/green/Dockerfile Blue-Green-Deployment/green'
      
			}
		}

		stage('Push Image To Dockerhub') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
						docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
						docker push levitehc/blueimage
					'''
				}
			}
		}
                        sh 'docker rmi -f levitech/greenimage'
                        sh 'docker rmi -f levitech/blueimage'
                    }
                }
    }
}
