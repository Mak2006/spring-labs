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

During the creation of the build we had marked Tomcat as provided. We want to package it along the application hence we remove `<scope>provided</scope>`

Insert dependency for the Google's Jib Maven plugin which we shall use to dockerise the applicaition. Google publishes **Jib** as both a **Maven** and a Gradle **plugin**. This **is** nice because it means that **Jib will** catch any changes we make to our application each time we build. This saves us separate docker build/push commands and simplifies adding this to a CI pipeline.

```
<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>jib-maven-plugin</artifactId>
  <version>0.9.6</version>
  <configuration>
	  <to>
      <image>gcr.io/[PROJECT_ID]/guestbook-frontend</image>
    </to>
  </configuration>
</plugin>

```
Our build now becomes
`./mvnw clean compile jib:build`

We now do the same for the backend service. That is remove Tomcat `provided` scope, add the Jib plugin and fire jib target. 

This completes our dockerization and we now set up the service account to use GKE.

### Set up service account to use GKE
```
// Set up service account
gcloud iam service-accounts create guestbook

export PROJECT_ID=$(gcloud config list --format 'value(core.project)')
gcloud projects add-iam-policy-binding ${PROJECT_ID} \
  --member serviceAccount:guestbook@${PROJECT_ID}.iam.gserviceaccount.com \
  --role roles/editor

// Generate JSon key
gcloud iam service-accounts keys create \ ~/service-account.json \ --iam-account guestbook@${PROJECT_ID}.iam.gserviceaccount.com

```

### Check and prepare the GKE
Check the Kubectl version 
`kubectl version`

// Add the secret
`kubectl create secret generic guestbook-service-account \ --from-file=$HOME/service-account.json`

//Check if the secret is available
`kubectl describe secret guestbook-service-account`

### Deploy the containers
// Create the yaml
// the file we modify is `~/kubernetes/guestbook-frontend-deployment.yaml`. 
// Replace the project id. 
the yaml now looks li


<!--stackedit_data:
eyJoaXN0b3J5IjpbNDE2NjI5NTI5LC00NzI0MDk4NTUsLTE5MD
A1NDk4NjJdfQ==
-->