# Cloud Docker Assignment

## About

Completed Assignment 3 for the Cloud Computing & Big Data
class at Columbia University and New York University, Fall 2023.

The project implements Docker, Kubernetes, Prometheus, and Alert Manager. 

Team members:
Anna Nefedenkova (an3143)
Shivam Shekhar (ss6960)

## Usage and Instructions

To run this app locally: 
1. Download and clone the repository.
2. Run the requirements files. 

Part 1.
If you run into any errors, a potential option could be updating your mongoDB with Brew (follow the instruction in this link: https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/#std-label-install-mdb-community-macos)
Another important update if working on a mac could be is to ensure that you have download the most up-to-date comand lines (thought Apple developer) (Command Line Tools for Xcode 15.1 beta 3)

Part 2.
Download Docker and create the image and the container for your app. 
- docker-compose up --build
To re-run the app and get the HTTP local link, run: 
- docker-compose up --no-build

To create and push a tag, run the following:
- docker login
- docker tag [IMAGENAME]:[IMAGETAG] [USERNAME]/[REPO] #cloud_docker--web:latest annancs/cloud-docker-kubrnt
- docker images
- docker push [newly created iamge]  #annancs/cloud-docker-kubrnt:latest    

Part 3.
Install your Minikube: 
- minikube start
Make sure you set up kompose on our machine first
- mkdir wp-manifests 
- mv docker-compose.yaml wp-manifests
- cd wp-manifests 
- kompose convert // will create the files used in the next command
- kubectl create -f mongo-data-persistentvolumeclaim.yaml,mongo-deployment.yaml,mongo-service.yaml,web-deployment.yaml,web-service.yaml
- minikube service web 
To view your creations:
- kubectl get pods -o wide
- kubectl get pvc
- kubectl get pv
- kubectl get deployments
- kubectl get svc 

You can check all your resources with this command:
- minikube dashboard 
To clean up creations: 
- kubectl delete [deployments OR pods OR else] --all
- kubectl delete -f [FILENAME]

PART 4: 

Make sure to have AWS installed: 
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

Make sure you have eksclt installed 
- eksctl create cluster -f eks-cluster.yaml
You can check your new cluster by running: 
- kubectl config get-clusters

Bug fixing, make sure all your architecture is the same between apps: 

- docker buildx build -t annancs/cloud-docker-kubrnt:amd64 --platform linux/amd64 .
- docker push annancs/cloud-docker-kubrnt:amd64

Before applications, files are slightly changed. 
- kubectl apply -f mongo-deployment.yaml,mongo-service.yaml,web-deployment.yaml,web-service.yaml
- kubeclt get svc
Now you can use the Amazon link of the service, add the post to it, and see your app.

Part 6: 
Again, ensure your architecture is up to date.
- docker buildx build -t annancs/cloud-docker-kubrnt:amd64v.2 --platform linux/amd64 .
- docker push annancs/cloud-docker-kubrnt:amd64

Part 8: 
Useful resources: 
https://devopscube.com/alert-manager-kubernetes-guide/#
https://devopscube.com/setup-kube-state-metrics/
https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/
https://grafana.com/blog/2020/02/25/step-by-step-guide-to-setting-up-prometheus-alertmanager-with-slack-pagerduty-and-gmail/#step-1-create-alerting-rules-in-prometheus

Useful commands: 
kubectl create -f clusterRole.yaml,config-map.yaml,prometheus-deployment.yaml,prometheus-service.yaml 
kubectl delete -f clusterRole.yaml,config-map.yaml,prometheus-deployment.yaml,prometheus-service.yaml 
kubectl create -f AlertManagerConfigmap.yaml,AlertTemplateConfigMap.yaml,Deployment.yaml,Service.yaml
kubectl delete -f AlertManagerConfigmap.yaml,AlertTemplateConfigMap.yaml,Deployment.yaml,Service.yaml
kubectl get deployments --namespace=monitoring
kubectl get pods --namespace=monitoring
for Prometheus:
kubectl port-forward [PROMPODNAME] 8080:9090 -n monitoring
for alert:
kubectl port-forward [ALERTPODNAME] 9093:9093 -n monitoring
