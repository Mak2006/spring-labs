# Cloud Pub/Sub integration

In this part of the series we integrate our application with Cloud Pub Sub

In this lab, you enhance your application to implement a message handling service with Cloud Pub/Sub so that it can publish a message to a topic that can then be subscribed and processed by other services.

Cloud Pub/Sub is a fully managed, real-time messaging service that enables you to send and receive messages between independent applications. Cloud Pub/Sub brings the scalability, flexibility, and reliability of enterprise message-oriented middleware to the cloud. By providing many-to-many, asynchronous messaging that decouples senders and receivers, Cloud Pub/Sub enables secure and highly available communication between independently written applications. Cloud Pub/Sub delivers low-latency, durable messaging that helps developers quickly integrate systems hosted on the Google Cloud Platform and externally.

## Steps
Here we note the important steps
### Enable Cloud Pub/Sub and create a Cloud Pub/Sub topic
    
-   Use Spring to add Cloud Pub/Sub support to your application
    
-   Modify an application to publish Cloud Pub/Sub messages
    
-   Create a Cloud Pub/Sub subscription
    
-   Modify an application to process messages from a Cloud Pub/Sub subscription
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjc0NjUzNDk3XX0=
-->