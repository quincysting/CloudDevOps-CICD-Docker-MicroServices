# Cloud DevOps Project5

## Project5 workflow

![img-1](Images/Workflow.jpg)

## Project5 environmet setup:

> PuTTY into instance ec2-54-188-126-103.us-west-2.compute.amazonaws.com and install

* Jenkins with Blue Ocean Plugin in Jenkins and Pipeline-AWS Plugin
* Docker (pre-insatlled)
* Pip
* AWS Cli
* Eksctl 0.15.0
* Kubectl

## Project5 github files:
```sh
Branch create_cluster :
Jenkinsfile : pipeline for creating Kubernetes cluster

Branch master :
* /Images : Screenshots of project5 
* Jenkinsfile : pipeline for deploying container
* Dockerfile : Dockerfile for building the image 
* green-controller.json : Create a replication controller green pod
* green-service.json : Create the green service
* blue-controller.json : Create a replication controller blue pod
* blue-service.json : Create the blue service
* index.html : HTML file
```

## Project5 flow:

> Create EC2 instance

![img-2](Images/Instance.JPG)

> Setup Jenkins

![img-3](Images/Jenkins.JPG)

> Create Kubernetes cluster pipeline

![img-4](Images/Create_Kubernetes_cluster_pipeline.JPG)

> Create cluster configuration

![img-5](Images/Create_cluster_configuration.JPG)

> CloudFormation cluster

![img-6](Images/CloudFormation_cluster.JPG)

> CloudFormation nodes

![img-7](Images/CloudFormation_nodes.JPG)

> Instance load balance

![img-8](Images/Instance_load_balance.JPG)

> Lint check index.html

![img-9](Images/Stage_lint_checkHTML.JPG)

> Build docker image

![img-10](Images/Stage_build_docker_image.JPG)

> Push docker image to docker.io

![img-11](Images/Stage_push_dockerhub.JPG)

> Image uploaded

![img-12](Images/Docker.JPG)

> Set EKS context to cluster arn:aws:eks:us-west-2:570781860922:cluster/proj5cluster

![img-13](Images/Stage_set_EKS_cluster.JPG)

> Deploy blue container

![img-14](Images/Stage_deploy_blue_container.JPG)

> Deploy green container

![img-15](Images/Stage_deploy_green_container.JPG)

> Create service in container

![img-16](Images/Stage_create_service_in_container.JPG)

> Wait for user approal to change over to green 

![img-17](Images/Stage_user_approval_to_change.JPG)

> Redirect to green 

![img-18](Images/Stage_redirect_to_green.JPG)

> Run "kubectl get services"

![img-19](Images/URL.png)

> Run "kubectl describe services bluegreenlb" to check service

![img-20](Images/URL1.png)

> Test service http://a293688adb09c4a36869328a2e3f73e0-727164161.us-west-2.elb.amazonaws.com:8000/

![img-21](Images/Mysite.JPG)

