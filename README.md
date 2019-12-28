AWS Blue and Green Deployment using Kubernetes Service and Docker and Jenkins

1. using amazon EC2 service to implement services such as Docker and Jenkins to be installed
2. getting the right requirment to launch your pipeline included a Jenkinsfile and Dockerfile
3. running your service using kubernetes and docker. Configure kubernete and Docker to sussucessfully deploy your service.

# Git Repository URL 

```
https://github.com/Levi-Tech/Udacity-Capstone-Project
```
# Spin up cluster

```
eksctl create cluster --name bluegreen2 --nodes=2 --region=us-west-2
aws --region us-west-2 eks update-kubeconfig --name bluegreen2
```

### create a replication controller blue pod and green

```
kubectl apply -f ./blue-controller.json
kubectl apply -f ./green-controller.json
```

### create the service, redirct to blue and make it externally visible

```
kubectl apply -f ./blue-green-service.json
```
### get the URL of the service 

```
Kubectl get svc
```

this should take you to green image on host. 

Successfully done will included Jenkinsfile, and blue-green deployment docker file, and images. 


