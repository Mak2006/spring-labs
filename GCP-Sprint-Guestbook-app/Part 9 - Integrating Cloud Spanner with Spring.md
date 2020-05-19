# Integrating Cloud Spanner with Spring
Cloud Spanner is an enterprise-grade, globally distributed, strongly consistent database service built for the cloud specifically to combine the benefits of relational database structure with non-relational horizontal scale. This combination delivers high-performance transactions and strong consistency across rows, regions, and continents with enterprise-grade security.

In this lab, you update your application to use the Spring Cloud GCP starter for Cloud Spanner, test the changes locally in Cloud Shell, and then redeploy the backend service to App Engine.

### Enable cloud spanner
`gcloud services enable spanner.googleapis.com`

### Create and provision a Cloud Spanner instance
Create a Cloud Spanner instance.
`gcloud spanner instances create guestbook --config=regional-us-central1 \ --nodes=1 --description="Guestbook messages`

Create a `messages` database in the Cloud Spanner instance.
`gcloud spanner databases create messages --instance=guestbook`

Confirm that the database exists by listing the databases of the Cloud Spanner instance.
`gcloud spanner databases list --instance=guestbook`

Create a table in the  `messages`  database by creating a file that contains a DDL statement and then running the command.
```
cd ~/guestbook-service 
mkdir db
vi spanner.ddl

``` 
### Use the data definition language (DDL) to create a Cloud Spanner table
    
### Use Spring to add support for Cloud Spanner to an application
    
### Modify a Java application to use Cloud Spanner instead of Cloud SQL
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2NjcwMzA1XX0=
-->