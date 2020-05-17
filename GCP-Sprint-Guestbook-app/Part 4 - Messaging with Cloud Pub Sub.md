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
Pub / Sub works on basis of topic, which serves as a channel for message flow. 

A topic can have multiple subscriptions. A subscription can have many subscribers. If you want to distribute different messages to different subscribers, then each subscriber needs to subscribe to its own subscription. If you want to publish the same messages to all the subscribers, then all the subscribers must subscribe to the same subscription.

Cloud Pub/Sub delivery is "at least once." Thus, you must deal with idempotence and you must deduplicate messages if you cannot process the same message more than once.

`gcloud pubsub subscriptions create messages-subscription-1 \ --topic=messages`

Test it by 
`gcloud pubsub subscriptions pull messages-subscription-1 --auto-ack` - pull a message - since topic is newly cfreated there would be no messages. Note the message remain in the subs untill it is acknowledged, so we set `--auto-ack`


    
### Create an application to process messages from a Cloud Pub/Sub subscription

Creating an app
```
cd ~ 
curl https://start.spring.io/starter.tgz \ -d dependencies=cloud-gcp-pubsub \ -d baseDir=message-processor | tar -xzvf -
```
add to the pom

```
<dependencies>
  <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-gcp-starter-pubsub</artifactId>
  </dependency>
  <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-test</artifactId>
       <scope>test</scope>
  </dependency>
</dependencies>

```
Write a class to consume the message
The imports
```
import org.springframework.context.annotation.Bean; import org.springframework.boot.CommandLineRunner; import org.springframework.cloud.gcp.pubsub.core.*;

```

The code

```
@Bean
public CommandLineRunner cli(PubSubTemplate pubSubTemplate) {
return (args) -> {
    pubSubTemplate.subscribe("messages-subscription-1",
       (msg, ackConsumer) -> {
	    System.out.println(msg.getData().toStringUtf8());
	    ackConsumer.ack();
       });
};
}
```

To test the code, we introduce themessages via the app and it gets pushed to the topic. Since our client is  a subscriber, it will get the message. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDI1NTM5ODEzLC0xOTQzOTA0NTg4LC05ND
Q2Nzg3NjAsOTA1NzcwNTgwLDk2MjU5MDc0NV19
-->