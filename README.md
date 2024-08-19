# Overview
This project involved the containerization and deployment of a full-stack yolo application using Docker.


# Requirements
Install the docker engine here:
- [Docker](https://docs.docker.com/engine/install/) 

## Deploy the application on kubernetes on Google Cloud

- Create and configure GKE cluster

`gcloud container clusters create --machine-type=e2-medium --zone=africa-south1-a --disk-size=10 yolo`
`gcloud container clusters --zone=africa-south1-a get-credentials yolo`

- Clone the repo

`git clone https://github.com/navi-da/yolo.git`

- Deploy the database
`kubectl create -f yolo/kubernetes/service/database-service.yaml`
`kubectl create -f kubernetes/deployment/database-deployment.yaml`

- Deploy the backend
`kubectl create -f yolo/kubernetes/service/backend-service.yaml`
`kubectl create -f yolo/kubernetes/deployment/backend-deployment.yaml`

- Deploy the frontend
`kubectl create -f yolo/kubernetes/service/frontend-service.yaml`
`kubectl create -f yolo/kubernetes/deployment/frontend-deployment.yaml`

- Run `kubectl get service yolo-client` to obtain the IP address for the frontend

- Access the application on your browser using the following URL
 `http://34.148.81.123:3000/`
