# App - Guestbook applciation
Application forked from Coursera Spring Course from Google. 
Repo - https://github.com/saturnism/spring-cloud-gcp-guestbook.git
## Stack 
1. Microservices communication - Rabbit MQ. 
1. Backend - MySQL
1. Microservice tracking - Zipkin

## Architecture
A client server app with 3 microservices Spring based.  
1. GUI
2. Config
3. Busines tier microservice. 

## Git
1. 

## Configuring and connecting to Cloud SQL
 1. Creating a db using Cloud SQL and access it from spring application. 
 2. Get a cloud shell
 3. `export PROJECT_ID=$(gcloud config list --format 'value(core.project)')`
 4.  use gsutil to access a cloud storage, 
 `gsutil ls gs://$PROJECT_ID`
 5.  use gsutil to copy the two microservices to local
`gsutil -m cp -r gs://$PROJECT_ID/* ~/`
 1.  Open the  cloud editor 
 2. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbNTg0NzEwMjk0LDEwNjk1NzEzNTMsLTYwMT
MyMTIzNF19
-->