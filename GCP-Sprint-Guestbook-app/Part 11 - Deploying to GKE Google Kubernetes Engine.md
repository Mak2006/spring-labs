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

![REMOVE provided](https://i.imgur.com/XTmkHkT.png)

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
![The JIB plugin ](https://i.imgur.com/SvI6eoy.png)

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

All goes well
![Kubectl init](https://i.imgur.com/pKkXuJR.png)

### Change the Yaml def for deploying the containers
// Create the yaml
// the file we modify is `~/kubernetes/guestbook-frontend-deployment.yaml`. 

Replace the line `image: saturnism/spring-gcp-guestbook-frontend:latest` with the line `image: gcr.io/[PROJECT_ID]/guestbook-frontend` below the line specifying the container name.

The yaml now looks like below  for the front end
```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: guestbook-frontend
  name: guestbook-frontend
spec:
  type: LoadBalancer
  ports:
  - name: http
    port: 8080
    targetPort: 8080
  selector:
    app: guestbook-frontend
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: guestbook-frontend
  name: guestbook-frontend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: guestbook-frontend
  template:
    metadata:
      labels:
        app: guestbook-frontend
    spec:
      volumes:
      - name: credentials
        secret:
          secretName: guestbook-service-account
      containers:
      - name: guestbook-frontend
        image: gcr.io/qwiklabs-gcp-04-12f91b960a09/guestbook-frontend
        volumeMounts:
        - name: credentials 
          mountPath: "/etc/credentials"
          readOnly: true
        env:
        - name: SPRING_CLOUD_CONFIG_ENABLED
          value: "false"
        - name: SPRING_CLOUD_GCP_CONFIG_ENABLED
          value: "false"
        - name: MESSAGES_ENDPOINT
          value: http://guestbook-service:8080/guestbookMessages
        - name: SPRING_PROFILES_ACTIVE
          value: cloud
        - name: GOOGLE_APPLICATION_CREDENTIALS
          value: /etc/credentials/service-account.json
        ports:
        - name: http
          containerPort: 8080

```
The service yaml is 

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: guestbook-service
  name: guestbook-service
spec:
  ports:
  - name: http
    port: 8080
    targetPort: 8080
  selector:
    app: guestbook-service
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: guestbook-service
  name: guestbook-service
spec:
  replicas: 2
  selector:
    matchLabels:
      app: guestbook-service
  template:
    metadata:
      labels:
        app: guestbook-service
    spec:
      volumes:
      - name: credentials
        secret:
          secretName: guestbook-service-account
      containers:
      - name: guestbook-service
        image: gcr.io/qwiklabs-gcp-04-12f91b960a09/guestbook-service
        volumeMounts:
        - name: credentials 
          mountPath: "/etc/credentials"
          readOnly: true
        env:
        - name: SPRING_PROFILES_ACTIVE
          value: cloud
        - name: GOOGLE_APPLICATION_CREDENTIALS
          value: /etc/credentials/service-account.json
        ports:
        - name: http
          containerPort: 8080

```

### Apply the yaml 
`kubectl apply -f ~/kubernetes/`
![enter image description here](https://i.imgur.com/S0uaVnS.png)

### Test 
`kubectl get svc guestbook-frontend`
`kubectl get svc`
get the external IP and launch



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUyMTk1MTY2MywtNDM1NjQxMjgxLDQ1MD
gwNzQyMywxOTIyMTYxMDM0LDIxMTk1NzUxOSwtODI4MTQwMjEx
LC00NzI0MDk4NTUsLTE5MDA1NDk4NjJdfQ==
-->