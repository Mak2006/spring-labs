# Monitoring the Google Kubernetics Engine with Prometheus

In tradtional Java world, for monitoring JMX, JProfiler etc were used. In the cloud centric world, tools like Prometheus is used. 

Cloud Kubernetes Monitoring aggregates logs, events, and metrics from your Kubernetes Engine environment to help you understand your application's behavior in production. Prometheus is an optional monitoring tool often used with Kubernetes. If you configure Cloud Kubernetes Monitoring with Prometheus support, then services that expose metrics using the Prometheus data model also have their data exported from the cluster and made visible as external metrics in Cloud Monitoring.

In this lab, you enable Prometheus monitoring for Kubernetes and then modify the demo application to expose Prometheus metrics from within the application and its backend service. You can then use Cloud Monitoring to monitor internal performance metrics from your application while it is running on Kubernetes Engine.

### Enable Cloud Monitoring for Kubernetes Engine
Load the Google Monitoring dashboard to create a monitoring workspace.  It shall take some time to load

![enter image description here](https://i.imgur.com/szg09Bf.png)

Once done we see a dashboard like as below
![Sample monitoring dashboard](https://i.imgur.com/LOwCjNX.png)


### Enable Prometheus monitoring in a Kubernetes Engine cluster
`gcloud container clusters get-credentials guestbook-cluster \ --zone=us-central1-a`

Install role-based access control for the Prometheus agent.
`kubectl apply -f \ https://storage.googleapis.com/stackdriver-prometheus-documentation/rbac-setup.yml \ --as=admin --as-group=system:masters`

Install the Prometheus agent.
```
export PROJECT_ID=$(gcloud config list --format 'value(core.project)')
curl -s \
https://storage.googleapis.com/stackdriver-prometheus-documentation/prometheus-service.yml | \
  sed -e "s/\(\s*_kubernetes_cluster_name:*\).*/\1 'guestbook-cluster'/g" | \
  sed -e "s/\(\s*_kubernetes_location:*\).*/\1 'us-central1'/g" | \
  sed -e "s/\(\s*_stackdriver_project_id:*\).*/\1 '${PROJECT_ID}'/g" | \
  kubectl apply -f -
```

Verify if prometheus is running 
`kubectl get pods -n stackdriver`


Here is the output 
![Prometheus init](https://i.imgur.com/5d56NX7.png)
### Expose Prometheus metrics from inside a Spring Boot application
Spring Boot can expose metrics information through Spring Boot Actuator. Micrometer is the metrics collection facility included in Spring Boot Actuator. Micrometer can expose all the metrics using the Prometheus format.

If you are not using Spring Boot, you can expose JMX metrics through Prometheus by using a  [Prometheus JMX Exporter agent](https://github.com/prometheus/jmx_exporter).

In this task, you add the Spring Boot Actuator starter and Micrometer dependencies to the guestbook frontend application.

Add the following to the pom of the application for the integration
```
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
     <groupId>io.micrometer</groupId>
     <artifactId>micrometer-registry-prometheus</artifactId>
     <scope>runtime</scope>
</dependency>

```
Below we incorporated the dependency
![Micrometer](https://i.imgur.com/FfkznPo.png)


In the Cloud Shell code editor, open  `~/guestbook-frontend/src/main/resources/application.properties`.

```
management.server.port=8081
management.endpoints.web.exposure.include=*
``` 
### Explore live application metrics using Cloud Monitoring
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczMTkwODI5OCwxMjAyMjUzOTQyLC0xNT
IyNTAyODcyLC0xOTQxMjY4MDI0LDEzNDEwNjk2NzhdfQ==
-->