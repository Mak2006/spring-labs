# Cloud Pub/Sub integration

In this part of the series we integrate our application with Cloud Pub Sub

In this lab, you enhance your application to implement a message handling service with Cloud Pub/Sub so that it can publish a message to a topic that can then be subscribed and processed by other services.

Cloud Pub/Sub is a fully managed, real-time messaging service that enables you to send and receive messages between independent applications. Cloud Pub/Sub brings the scalability, flexibility, and reliability of enterprise message-oriented middleware to the cloud. By providing many-to-many, asynchronous messaging that decouples senders and receivers, Cloud Pub/Sub enables secure and highly available communication between independently written applications. Cloud Pub/Sub delivers low-latency, durable messaging that helps developers quickly integrate systems hosted on the Google Cloud Platform and externally.

## Steps
### Enable Cloud Pub/Sub 
`gcloud services enable pubsub.googleapis.com`  

### Create a topic
gcloud pubsub topics create messages

### Add to applciation using Spring starter
```
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-gcp-starter-pubsub</artifactId>
</dependency>

```
### Write code to publish Cloud Pub/Sub messages
```
import org.springframework.cloud.gcp.pubsub.core.*;


@Autowired private 
PubSubTemplate pubSubTemplate;

/*Fire the message*/
pubSubTemplate.publish("messages", name + ": " + message);
```
    
### Create a Cloud Pub/Sub subscription

    
### Modify an application to process messages from a Cloud Pub/Sub subscription
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjM4NjU1Njk2LDkwNTc3MDU4MCw5NjI1OT
A3NDVdfQ==
-->