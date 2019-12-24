AWS Blue and Green Deployment using Kubernetes Service and Docker

1. using amazon EC2 service to implement services such as Docker and Jenkins to be installed
2. getting the right requirment to launch your pipeline included a Jenkinsfile and Dockerfile
3. running your service using kubernetes and docker. Configure kubernete and Docker to sussucessfully deploy your service.
# ./run_docker.sh
# ./upload_docker.sh
#create a replication controller blue pod and green
kubectl apply -f ./blue-controller.json
kubectl apply -f ./green-controller.json
#create the service, redirct to blue and make it externally visible
kubectl apply -f ./blue-green-service.json
#get the URL of the service by running
minikube service bluegreenlb --url
this should take you to green image on host. 

Successfully done will included Jenkinsfile, and blue-green deployment docker file, and images. 


