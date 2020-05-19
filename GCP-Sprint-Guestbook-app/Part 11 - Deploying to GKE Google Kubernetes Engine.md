# Deploying to Google Kubernetes Engine

Kubernetes Engine is Google's managed, production-ready environment for deploying containerized applications. Kubernetes Engine enables rapid application development and iteration by making it easy to deploy, update, and manage your applications and services. Kubernetes Engine enables you to quickly get up and running with Kubernetes by eliminating the need to install, manage, and operate your own Kubernetes clusters.

In this lab, you build the application into a container and then deploy the containerized application to Kubernetes Engine.

###  Enable and create Google Kubernetes Engine 
`gcloud services enable container.googleapis.com`

Create a Kubernetes Engine cluster
```
gcloud container clusters create guestbook-cluster \
    --zone=us-central1-a \
    --num-nodes=2 \
    --machine-type=n1-standard-2 \
    --enable-autorepair \
    --enable-cloud-monitoring \
    --enable-cloud-logging
```

### Create a containerized version of a Java application
Enable container registry
`gcloud services enable containerregistry.googleapis.com`
`gcloud config list --format 'value(core.project)'`

Since the app was running on Tomcat 

### Create a Kubernetes deployment for a containerized application
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MjYyODE3LC0xOTAwNTQ5ODYyXX0=
-->