# Spring Runtime Configurations

1. In a production environment, you need a robust mechanism to store and update configuration values that might change dynamically. Typically, you end up with additional configuration servers that you have to make highly available and manage yourself. Cloud Runtime Configuration API enables you to define and store data as a hierarchy of key-value pairs in Google Cloud Platform (GCP). You can use these key-value pairs to dynamically configure services, communicate service states, send notification of changes to data, and share information between multiple tiers of service.
2. Spring Cloud GCP has a configuration starter that interoperates well with the Spring Cloud Config facility. This starter enables you to integrate runtime configuration capabilities into your applications without having to manually build and manage your own configuration server.
## Steps
4. Use Spring Cloud GCP to add support for Cloud Runtime Configuration API. This is added to the microservice require the aspect .  In the pom.xml
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
6.  Create deployment profiles to selectively enable support for runtime configuration services
Enable the dynamic refresh of runtime configuration values in an application
Use Cloud Runtime Configuration API to create runtime configuration profiles and values
Use Cloud Runtime Configuration API to dynamically update an application setting
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNTg0NjMyOTUsLTc1OTg1MjQ0NCwtMj
A4ODc0NjYxMl19
-->