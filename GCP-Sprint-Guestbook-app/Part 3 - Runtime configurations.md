# Spring Runtime Configurations

1. In a production environment, you need a robust mechanism to store and update configuration values that might change dynamically. Typically, you end up with additional configuration servers that you have to make highly available and manage yourself. Cloud Runtime Configuration API enables you to define and store data as a hierarchy of key-value pairs in Google Cloud Platform (GCP). You can use these key-value pairs to dynamically configure services, communicate service states, send notification of changes to data, and share information between multiple tiers of service.
2. Spring Cloud GCP has a configuration starter that interoperates well with the Spring Cloud Config facility. This starter enables you to integrate runtime configuration capabilities into your applications without having to manually build and manage your own configuration server.
3. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc1OTg1MjQ0NCwtMjA4ODc0NjYxMl19
-->