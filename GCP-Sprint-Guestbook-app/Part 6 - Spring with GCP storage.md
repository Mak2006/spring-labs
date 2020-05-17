In this lab we create a form and upload an image, which gets stored in Cloud storage. Later we read it from there and display it. 

Google Cloud Platform (GPC) has a bucket-based object storage solution called Cloud Storage. Cloud Storage provides fast, low-cost, highly durable, global object storage for developers and enterprises that need to manage unstructured file data. In Cloud Storage, the consistent API, low latency, and speed across storage classes simplify development integration and reduce code complexity.

### Add the Spring starter for Cloud Storage
We do this in the appliation that requires cloud storage. Include the dependency
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-gcp-starter-storage</artifactId>
</dependency>

```
### Create a Cloud Storage bucket
 This is done manually in this lab. And we shall use it from the code. 

### Uploading files to it. 
We create a form where the user can upload the file and p

-      
-   Modify the HTML template of the frontend application to enable file uploads
    
-   Modify the frontend application to process and store images on Cloud Storage
    
-   Modify the frontend application to display uploaded message images
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwMDgyMDE2NSwtMTgxMzQ1NzE2OV19
-->