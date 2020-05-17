# Spring Runtime Configurations

1. In a production environment, you need a robust mechanism to store and update configuration values that might change dynamically. Typically, you end up with additional configuration servers that you have to make highly available and manage yourself. Cloud Runtime Configuration API enables you to define and store data as a hierarchy of key-value pairs in Google Cloud Platform (GCP). You can use these key-value pairs to dynamically configure services, communicate service states, send notification of changes to data, and share information between multiple tiers of service.
2. Spring Cloud GCP has a configuration starter that interoperates well with the Spring Cloud Config facility. This starter enables you to integrate runtime configuration capabilities into your applications without having to manually build and manage your own configuration server.
## Steps
1.  **Configurations -** Use Spring Cloud GCP to add support for Cloud Runtime Configuration API. This is added to the microservice require the aspect .  In the pom.xml
```
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-gcp-starter-config</artifactId>
</dependency>
<dependency>
   <groupId>com.google.guava</groupId>
   <artifactId>guava</artifactId>
   <version>20.0</version>
</dependency>
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
and this 
```
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-gcp-dependencies</artifactId>
<version>1.1.0.M1</version>
<type>pom</type>
<scope>import</scope>
</dependency>

```
and teh repository
```
<repositories>
 <repository>
      <id>spring-milestones</id>
      <name>Spring Milestones</name>
      <url>https://repo.spring.io/milestone</url>
      <snapshots>
	  <enabled>false</enabled>
      </snapshots>
 </repository>
</repositories>

```
2. For local testing this service can be disabled. Use 
`spring.cloud.gcp.config.enabled=false`  in the application properties

3.  Create deployment profiles to selectively enable support for runtime configuration services. Profiles another level of hierarchy. Example 

Open  `guestbook-frontend/src/main/resources/bootstrap-cloud.properties`  in the Cloud Shell code editor and add the following new properties:
```
spring.cloud.gcp.config.enabled=true
spring.cloud.gcp.config.name=frontend
spring.cloud.gcp.config.profile=cloud
```

5. Enable the dynamic refresh of runtime configuration values in an application. 
By default, runtime configuration values are read only when an application starts. In this task, you add a Spring Cloud Config `RefreshScope` to the frontend application so that runtime configuration values can be updated dynamically without restarting the application. You do this by adding an `@RefreshScope` annotation to the `FrontendController` source file.

	1.  Insert the following lines below the import directives just above  `@Controller`:
    

```
import org.springframework.cloud.context.config.annotation.RefreshScope;

@RefreshScope
```

7. Use Cloud Runtime Configuration API to create runtime configuration profiles and values

Use Cloud Runtime Configuration API to dynamically update an application setting
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzOTc3NzAwNiwtMTk1NTU5MjM2MCwtMT
A1ODQ2MzI5NSwtNzU5ODUyNDQ0LC0yMDg4NzQ2NjEyXX0=
-->