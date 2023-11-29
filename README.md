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

After installing your Minikube: 
- minikube start

to continue with deployemnt: 
# make sure you est up kompose on our machine first
- mkdir wp-manifests 
- mv docker-compose.yaml wp-manifests
- cd wp-manifests 
- kompose convert 
kubectl create -f mongo-data-persistentvolumeclaim.yaml,mongo-deployment.yaml,mongo-service.yaml,web-deployment.yaml,web-service.yaml
- minikube service web 
to view your creations:
- kubectl get pods -o wide
- kubectl get pvc
- kubectl get pv
- kubectl get deployments
- kubectl get svc 

you can check all your resources with this command:
- minikube dashboard 

to clean up creations: 
- kubectl delete deployments OR pods --all

PART 4: 

makes sure to have aws installed: 
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

run:
Make sure you have eksclt installed 
- eksclt crea cluster with the yaml file


<!-- - aws configure
- aws eks update-kubeconfig \
  	--region us-east-2 \
  	--name EKScluster -->

you can check your new cluster by running: 
- kubectl config get-clusters

- kubectl create -f eks-deployment.yaml,eks-service.yaml

<!-- update the config for your cluster: 
- aws eks --region us-east-2 update-kubeconfig --name [EKD cluster name] -->


kubectl expose deployment eks --type=LoadBalancer --name=exposed