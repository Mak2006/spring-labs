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

### Configuring and connecting to Cloud SQL
 1. Creating a db using Cloud SQL and access it from spring application. 
 2. Get a cloud shell
 3. `export PROJECT_ID=$(gcloud config list --format 'value(core.project)')`
 4.  use gsutil to access a cloud storage, 
 `gsutil ls gs://$PROJECT_ID`
 5.  use gsutil to copy the two microservices to local
`gsutil -m cp -r gs://$PROJECT_ID/* ~/`
### Create a Cloud SQL instance, database, and table
 1.  Open the  cloud editor 
 2.  Enable cloud API 
`gcloud services enable sqladmin.googleapis.com`
 4.  Confirm that API is enabled
 `gcloud services list | grep sqladmin`
 5. List the cloud instances
 `gcloud sql instances list`, there are no instances yet and we shall provision one. 
 6.  Provision a new Cloud SQL instance.
 `gcloud sql instances create guestbook --region=us-central1` 
This would show like this
Provisioning the Cloud SQL instance will take a couple of minutes to complete.
```bash
Creating Cloud SQL instance...done.
Created [...].
NAME       DATABASE_VERSION REGION       TIER              ADDRESS   STATUS
guestbook  MYSQL_5_6        us-central1  db-n1-standard-1  92.3.4.5  RUNNABLE
```
11. Create a  `messages`  database in the MySQL instance. 
```
gcloud sql databases create messages --instance guestbook
```
12. The Cloud SQL is not able to connect from public IP
	1. -   Use a local Cloud SQL proxy.
	2. -   Use  `gcloud`  to connect through a CLI client.
	3. -   From the Java application, use the MySQL JDBC driver with an SSL socket factory for secured connection.
	4. We use the gloud method `gcloud sql connect guestbook` After this it is in SQL territory.
13.  Show the db's `mysql> show databases;`
14.  Use the messages db `use messages;`
15.  We fire a create sql now. 
```
CREATE TABLE guestbook_message (
  id BIGINT NOT NULL AUTO_INCREMENT,
  name CHAR(128) NOT NULL,
  message CHAR(255),
  image_uri CHAR(255),
  PRIMARY KEY (id)
);

```  and we exit the mysql prompt. 
### Use Spring to add Cloud SQL support to your application
17.  To connet we use the starter - `spring-cloud-gcp-dependencies` we add this to the pom.xml, we head to the cloud editor and add the dependency. Now the front end would not require this so this would be the back end service i.e., guestbook-service/pom.xml
`<groupId>org.springframework.cloud</groupId> `
`<artifactId>spring-cloud-gcp-dependencies</artifactId>` 
`<scope>import</scope>`
18.  Insert mysql dependency 
``
<dependency> <groupId>org.springframework.cloud</groupId> 
<artifactId>spring-cloud-gcp-starter-sql-mysql</artifactId>
</dependency>
``
19. 4.  Insert a new section called  `<repositories>`  at the bottom of the file, after the  `<build>`  section and just before the closing  `</project>`  tag.
    

```
        <repositories>
                <repository>
                        <id>spring-milestones</id>
                        <name>Spring Milestones</name>
                        <url>https://repo.spring.io/libs-milestone</url>
                        <snapshots>
                                <enabled>false</enabled>
                        </snapshots>
                </repository>
        </repositories>

20. ### **Disable Cloud SQL in the default profile**

For local testing, you can continue to use a local database or an embedded database. The demo application is initially configured to use an embedded HSQL database.

To continue to use the demo application for local runs, you disable the Cloud SQL starter in the default application profile by updating the  `application.properties`  file.

1.  In the Cloud Shell code editor, open  `guestbook-service/src/main/resources/application.properties`.
2. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2NDE3NTA2Myw2MDE1NDUxMDUsLTYzND
M2NTU0MSw1ODQ3MTAyOTQsMTA2OTU3MTM1MywtNjAxMzIxMjM0
XX0=
-->