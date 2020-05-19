# Integrating Cloud Spanner with Spring
This series is a 12 part series in creating Spring application with GCP services. These are the notes that was created as part of coursework for the course titled Building Scalable Java Microservices with Spring Boot and Spring Cloud!

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
# Add the following ddl
CREATE TABLE guestbook_message (
    id STRING(36) NOT NULL,
    name STRING(255) NOT NULL,
    image_uri STRING(255),
    message STRING(255)
) PRIMARY KEY (id);
``` 
Run the ddl
`gcloud spanner databases ddl update messages \ --instance=guestbook --ddl="$(<db/spanner.ddl)"`

Open Spanner Dashboard, check Guestbook messages,  and table. There is no data yet. 

### Add Cloud Spanner to our app using Spring Starter
We add this to the backend as it is where app would talk tothe DB
```
<dependency>
     <groupId>org.springframework.cloud</groupId>
     <artifactId>spring-cloud-gcp-starter-data-spanner</artifactId>
</dependency>

```
Configure the profile to be used by the application. Open ~/`guestbook-service/src/main/resources/application-cloud.properties`. Add

```
spring.cloud.gcp.spanner.instance-id=guestbook spring.cloud.gcp.spanner.database=messages
```
All set we now create the ORM parts
###  Backend ORM part
Create file `~/guestbook-service/src/main/java/com/example/guestbook/GuestbookMessage.java`.

Add the following 

```
package com.example.guestbook;

import lombok.*;
import org.springframework.cloud.gcp.data.spanner.core.mapping.*;
import org.springframework.data.annotation.Id;

@Data
@Table(name = "guestbook_message")
public class GuestbookMessage {
        @PrimaryKey
        @Id
        private String id;

        private String name;

        private String message;

        @Column(name = "image_uri")
        private String imageUri;

        public GuestbookMessage() {
                this.id = java.util.UUID.randomUUID().toString();
        }
}
```
 At this stage it is more like ORM db manipulation and is not so much Spanner specific.  Spring Data Spanner implements many commonly used Spring Data patterns, such as creating simple methods that can be automatically translated to corresponding SQL queries.

As an example , we update the `GuestbookMessageRepository.java` file to use `String` as the ID type.
```
import java.util.List;

public interface GuestbookMessageRepository extends
        PagingAndSortingRepository<GuestbookMessage, String> {
        List<GuestbookMessage> findByName(String name);
}
```
 
 ### Testing the app
 Run
 `./mvnw spring-boot:run -Dserver.port=8081 -Dspring.profiles.active=cloud`

We now post some messages and check the spanner dashboard. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM3MjE2NTA0NCwyMDU1MTQ1MDZdfQ==
-->