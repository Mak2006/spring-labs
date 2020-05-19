# Monitoring the Google Kubernetics Engine with Prometheus

In tradtional Java world, for monitoring JMX, JProfiler etc were used. In the cloud centric world, tools like Prometheus is used. 

Cloud Kubernetes Monitoring aggregates logs, events, and metrics from your Kubernetes Engine environment to help you understand your application's behavior in production. Prometheus is an optional monitoring tool often used with Kubernetes. If you configure Cloud Kubernetes Monitoring with Prometheus support, then services that expose metrics using the Prometheus data model also have their data exported from the cluster and made visible as external metrics in Cloud Monitoring.

In this lab, you enable Prometheus monitoring for Kubernetes and then modify the demo application to expose Prometheus metrics from within the application and its backend service. You can then use Cloud Monitoring to monitor internal performance metrics from your application while it is running on Kubernetes Engine.

### Enable Cloud Monitoring for Kubernetes Engine
Load the Google Monitoring dashboard to create a monitoring workspace.  It shall take some time to load

![enter image description here](https://i.imgur.com/szg09Bf.png)

Once done we see a dashboard like as below
![enter image description here](https://i.imgur.com/LOwCjNX.png)



### Enable Prometheus monitoring in a Kubernetes Engine cluster
### Expose Prometheus metrics from inside a Spring Boot application
### Explore live application metrics using Cloud Monitoring
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NDEyNjgwMjQsMTM0MTA2OTY3OF19
-->