## Microservice Tracing with Zipkin and Spring Cloud Sleuth
In a microservices architecture, you need distributed tracing to make complicated service calls more visible. For example, when service A calls B, and B calls C, which service has a problem? In Spring Cloud GCP, you can easily add distributed tracing by using Spring Cloud Sleuth. This typically requires you to run and operate your own Zipkin backend.

In this lab, you implement distributed tracing by using Spring Cloud GCP, Spring Cloud Sleuth, and Cloud Trace. Spring Cloud GCP provides a starter that can interoperate with Spring Cloud Sleuth, but it forwards the trace request to Cloud Trace instead.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxNTMwMzc5NCw1MTgzMDgzMTZdfQ==
-->