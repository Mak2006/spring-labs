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
## Defining a parameter
 Use Cloud Runtime Configuration API to create runtime configuration profiles and values
 1.  In the Cloud Shell enable Cloud Runtime Configuration API.
    

```
gcloud services enable runtimeconfig.googleapis.com

```

2.  Create a runtime configuration for the frontend application's  `cloud`  profile.
    

```
gcloud beta runtime-config configs create frontend_cloud

```

A URL for the new runtime configuration similar to the following is displayed:

```bash
Created [https://runtimec.../v1beta1/projects/.../frontend_cloud].
```

3.  Set a new configuration value for the greeting message.
    

```
gcloud beta runtime-config configs variables set greeting \
  "Hi from Runtime Config" \
  --config-name frontend_cloud

```

4.  Enter the following command to display all the variables in the runtime configuration:
    

```
gcloud beta runtime-config configs variables list --config-name=frontend_cloud

```

5.  Enter the following command to display the value of a specific variable.
    

```
gcloud beta runtime-config configs variables \
  get-value greeting --config-name=frontend_cloud

```

The command displays the value of  `greeting`.


### Dynamically update a value
Use Cloud Runtime Configuration API to dynamically update an application setting

Open a new Cloud Shell tab and update the  `greeting`  configuration value:
    

```
gcloud beta runtime-config configs variables set greeting \
  "Hi from Updated Config" \
  --config-name frontend_cloud

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxMDE2MzczNiwxMzM5Nzc3MDA2LC0xOT
U1NTkyMzYwLC0xMDU4NDYzMjk1LC03NTk4NTI0NDQsLTIwODg3
NDY2MTJdfQ==
-->