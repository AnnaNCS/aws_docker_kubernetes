# Cloud Docker Assignment

```
1. Anna Nefedenkova
2. Shivam Shekhar
```


In order to run this app locally: 
Download and clone the repository.
Run the requirmnets files. 
If you run into any errors, a potential oslution could be updating your mongoDB with brew (follow the instruction in this link: https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/#std-label-install-mdb-community-macos)
Another important update if working on a mac could be is to ensure that you ave donwloa the most up to date comand lines (thought apple developer) (Command Line Tools for Xcode 15.1 beta 3)

Next, download docker and create the image and the container for your app. 
- docker-compose up --build

Laslty, to re-run the app and get the http local link, run: 
- docker-compose up --no-build

TO create and push a tga, run the following:
- docker login
- docker tag [IMAGENAME]:[IMAGETAG] [USERNAME]/[REPO] #cloud_docker--web:latest annancs/cloud-docker-kubrnt
- docker images
- docker push [newly created iamge]  #annancs/cloud-docker-kubrnt:latest    

After installing your Minikube, you can use the following commands to check on your deployemnst and pods: 
- kubectl get nodes
- kubectl get deployments  
- kubectl get pods -o wide

to continue with deployemnt: 
- kubectl create -f taskapp-dep.yaml 
- kubectl scale deployment tasksapp --replicas=3
- kubectl get pods -o wide
- kubectl create -f taskapp-svc.yaml 
- kubectl get svc tasksapp-svc
- kubectl create -f mongo-pv.yaml
- kubectl get pv
- kubectl create -f mongo-pvc.yaml
- kubectl get pvc
- kubectl get pv
- kubectl create -f mongo-dep.yaml 
- kubectl get deployments
- kubectl create -f mongo-svc.yaml
- kubectl get svc mongo

you can check all your resources with this command:
- minikube dashboard 

to clean up use: 
- kubectl delete deployments OR pods --all
