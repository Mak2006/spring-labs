# Using Spring to access Cloud Pub/Sub

In this lab, you use **Spring Integration** to create a message gateway interface that abstracts from the underlying messaging system rather than using direct integration with Cloud Pub/Sub.

Using this approach, you can swap messaging middleware that works with on-premises applications for messaging middleware that works with cloud-based applications. This approach also makes it easy to migrate between messaging middlewares.

In this lab, you use Spring Integration to add the message gateway interface and then refactor the code to use this interface rather than implementing direct integration with Cloud Pub/Sub.

###  Adding Spring Integration Core to an application
to the application pom.xml of the application add 
```
<dependency>
    <groupId>org.springframework.integration</groupId>
    <artifactId>spring-integration-core</artifactId>
</dependency>
```
    
-   Create an outbound message gateway in your application
    
-   Configure an application to publish messages through a gateway
    
-   Bind the output channel of a message gateway to Cloud Pub/Sub
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzU3NjQxN119
-->