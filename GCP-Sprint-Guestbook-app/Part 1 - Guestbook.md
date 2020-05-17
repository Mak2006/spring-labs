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

### Creating an applicatoin with Sprint Initializer 

`cd ~ curl https://start.spring.io/starter.tgz  -d dependencies=cloud-gcp-pubsub  -d baseDir=message-processor | tar -xzvf -`


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
<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-gcp-starter-sql-mysql -->
``<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-gcp-starter-sql-mysql</artifactId>
    <version>1.0.0.M2</version>
</dependency>
```
**Make sure the version is included **

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

20. ### Disable Cloud SQL in the default profile

For local testing, you can continue to use a local database or an embedded database. The demo application is initially configured to use an embedded HSQL database.

To continue to use the demo application for local runs, you disable the Cloud SQL starter in the default application profile by updating the  `application.properties`  file.

1.  In the Cloud Shell code editor, open  `guestbook-service/src/main/resources/application.properties`.  
2. add the property 
`spring.cloud.gcp.sql.enabled=false`

### Configure an application profile to use Cloud SQL

In this task, you create an application profile that contains the properties that are required by the Spring Boot Cloud SQL starter to connect to your Cloud SQL database.

### Configure a cloud profile

When deploying the demo application into the cloud, you want to use the production-managed Cloud SQL instance.

You create an application profile called  `cloud`  profile. The  `cloud`  profile leaves the Cloud SQL starter that is defined in the Spring configuration profile enabled. And it includes properties used by the Cloud SQL starter to provide the connection details for your Cloud SQL instance and database.

1.  In the Cloud Shell find the instance connection name by running the following command

```
gcloud sql instances describe guestbook --format='value(connectionName)'

```
This command format filters out the  `connectionName`  property from the description of the guestbook Cloud SQL object. The entire string that is returned is the instance's connection name. The string looks like the following example:

```bash
qwiklabs-gcp-4d0ab38f9ff2cc4c:us-central1:guestbook
```

2.  In the Cloud Shell code editor create an  `application-cloud.properties`  file in the  `guestbook-service/src/main/resources`  directory.
    
3.  In the Cloud Shell code editor, open  `guestbook-service/src/main/resources/application-cloud.properties`  and add the following properties:

```
spring.cloud.gcp.sql.enabled=true
spring.cloud.gcp.sql.database-name=messages
spring.cloud.gcp.sql.instance-connection-name=YOUR_INSTANCE_CONNECTION_NAME

```

4.  Replace the  `YOUR_INSTANCE_CONNECTION_NAME`  placeholder with the full connection name string returned in step 1 in this task.

If you worked in the Cloud Shell code editor, you screen looks like the following screenshot:

![c4982aa035f41b4.png](https://cdn.qwiklabs.com/4NXlfD3Um12BJUwXBz5jWuURH%2FXSTfAayCUx970XCag%3D)

### Configure the connection pool

You use the  `spring.datasource.*`  configuration properties to configure the JDBC connection pool, as you do with other Spring Boot applications.

1.  Add the following property to  `guestbook-service/src/main/resources/application-cloud.properties`  that should still be open in the Cloud Shell code editor to specify the connection pool size.
  

```
spring.datasource.hikari.maximum-pool-size=5

```

### **Test the backend service running on Cloud SQL**

You relaunch the backend service for the demo application in Cloud Shell, using the new cloud profile that configures the service to use Cloud SQL instead of the embedded HSQL database.

1.  In the Cloud Shell change to the  `guestbook-service`  directory.
    

```
cd ~/guestbook-service

```

2.  Start the backend service application with the  `cloud`  profile.
    
**Change the mvnw to executable - chmod 700 mvnw**

```
./mvnw spring-boot:run -Dserver.port=8081 -Dspring.profiles.active=cloud

```

3.  Verify that Cloud SQL connection logs appear during the application startup.
    

```
... First Cloud SQL connection, generating RSA key pair.
... Obtaining ephemeral certificate for Cloud SQL instance [springone17-sfo-1000:us-ce
... Connecting to Cloud SQL instance [...:us-central1:guestbook] on ...
... Connecting to Cloud SQL instance [...:us-central1:guestbook] on ...
... Connecting to Cloud SQL instance [...:us-central1:guestbook] on ...
...

```

4.  Open a new Cloud Shell tab and use  `curl`  to make a few calls.
    

```
curl -XPOST -H "content-type: application/json" \
  -d '{"name": "Ray", "message": "Hello Cloud SQL"}' \
  http://localhost:8081/guestbookMessages

```

5.  List all the messages.
    

```
curl http://localhost:8081/guestbookMessages

```

6.  Use the Cloud SQL client to validate that message records have been added to the database.
    

```
gcloud sql connect guestbook

```

7.  Press ENTER at the Enter password prompt.
    

```bash
Whitelisting your IP for incoming connection for 5 minutes...done.
Connecting to database with SQL user [root].Enter password:
```

8.  Query the  `guestbook_message`  table in the messages database.
    

```
use messages
select * from guestbook_message;

```

The  `guestbook_messages`  table now contains a record of the test message that you sent using  `curl`  in a previous step.

```bash
+----+------+----------------+-----------+
| id | name | message        | image_uri |
+----+------+----------------+-----------+
|  1 | Ray  | Hello Cloud SQL | NULL      |
+----+------+----------------+-----------+
1 row in set (0.04 sec)
```

9.  Close the Cloud SQL interactive client.
    

```
exit;

```


Our project id was 
qwiklabs-gcp-04-94261e73db16:us-central1:guestbook

Had to change the jvm, as the project was created in java 8 while the shell was different. 
sudo update-java-alternatives -s java-1.8.0-openjdk-amd64 && export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI0Nzk5ODYwMSw2MTc2MjQzODJdfQ==
-->