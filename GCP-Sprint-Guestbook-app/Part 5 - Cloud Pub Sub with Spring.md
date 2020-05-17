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
    
### Create an outbound message gateway in your application
```
package com.example.frontend;

import org.springframework.integration.annotation.MessagingGateway;

@MessagingGateway(defaultRequestChannel = "messagesOutputChannel")
public interface OutboundGateway {
        void publishMessage(String message);
}
```
    
### Publish messages from an application through a gateway
The trigger could be from any where. The application decid
    
-   Bind the output channel of a message gateway to Cloud Pub/Sub
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY5MDU5MzgwNywxNzM0NDg5ODQ0XX0=
-->