## Microservice Tracing with Zipkin and Spring Cloud Sleuth
In a microservices architecture, you need distributed tracing to make complicated service calls more visible. For example, when service A calls B, and B calls C, which service has a problem? In Spring Cloud GCP, you can easily add distributed tracing by using Spring Cloud Sleuth. This typically requires you to run and operate your own Zipkin backend.

In this lab, we implement distributed tracing by using Spring Cloud GCP, Spring Cloud Sleuth, and Cloud Trace. Spring Cloud GCP provides a starter that can interoperate with Spring Cloud Sleuth, but it forwards the trace request to Cloud Trace instead.

Cloud Trace is a distributed tracing system that collects latency data from your applications and displays it in the Google Cloud Platform (GCP) console. You can track how requests propagate through your application and receive detailed, near-real-time performance insights. loud Trace automatically analyzes all of your application's traces to generate in-depth latency reports to surface performance degradations. And it can capture traces from all of your VMs, containers, or App Engine projects.

Language-specific SDKs for Cloud Trace can analyze projects running on VMs (even those not managed by GCP). The Trace SDK is currently available for Java, Node.js, Ruby, and Go. And Cloud Trace API can be used to submit and retrieve trace data from any source. A Zipkin collector is also available, which enables Zipkin tracers to submit data to Cloud Trace. Projects running on App Engine are automatically captured.

## Steps

 1. Enable Cloud Trace API 
 `gcloud services enable cloudtrace.googleapis.com`
 
 2. Use Spring to add Cloud Trace to your application. Add the following starter. 
 ```
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-gcp-starter-trace</artifactId>
</dependency>

 ```
 and 
 ```
 <dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-gcp-starter-trace</artifactId>
</dependency>

 ```
 4. Configure customized trace settings in an application.
		 1. Disable trace for dev purpose
		 2. 
 6. Inspect the trace output

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTk4NDc3OTE5LC04MTUzMDM3OTQsNTE4Mz
A4MzE2XX0=
-->