# Using Spring to access Cloud Pub/Sub
This series is a 12 part series in creating Spring application with GCP services. These are the notes that was created as part of coursework for the course titled Building Scalable Java Microservices with Spring Boot and Spring Cloud!

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
    
### Create an outbound message gateway Class in your application
```
package com.example.frontend;

import org.springframework.integration.annotation.MessagingGateway;
/* this is class OutboundGateway.java , it defines a method to publish the message. It uses the messagesOutputChannel to send the messages.
*/
@MessagingGateway(defaultRequestChannel = "messagesOutputChannel")
public interface OutboundGateway {
        void publishMessage(String message);
}
```

### Configure the channel to Pub/Sub
We do this in any starter / configuration class. 
```
import org.springframework.context.annotation.*; import org.springframework.cloud.gcp.pubsub.core.*; import org.springframework.cloud.gcp.pubsub.integration.outbound.*; import org.springframework.integration.annotation.*; import org.springframework.messaging.*;

/* Define the channel bean */
@Bean @ServiceActivator(inputChannel = "messagesOutputChannel") public MessageHandler messageSender(PubSubTemplate pubsubTemplate) { return new PubSubMessageHandler(pubsubTemplate, "messages"); }


```
This is also possible by external configuration. 
    
### Publish messages from an application through a gateway
The trigger could be from any where. The application decides when to post. To post to the outboud gateway we do the following 
```
/* get the gateway class we created */
@Autowired private OutboundGateway outboundGateway;

/* fire the message */
outboundGateway.publishMessage(name + ": " + message);
```
So we post a message now from the browser and can see the message in the channel. Here is a snanshot  
![enter image description here](https://i.imgur.com/uh8licH.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ4MjcxNzM1NywxNTQ3NTg0NDQ3LDE3MT
cwMjQ5MTMsLTYzNTE2NjcyNSwxNzM0NDg5ODQ0XX0=
-->