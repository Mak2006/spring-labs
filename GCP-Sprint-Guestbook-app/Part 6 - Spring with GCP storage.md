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

### Creating the UI. 
We create a form where the user can upload the file and post it. 

```
1. the form now takes multipart data hence we use
<form action="/post" method="post" enctype="multipart/form-data">

2. The input becomes
<!-- Add a file input --> 
<span>File:</span>
<input type="file" name="file" accept=".jpg, image/jpeg"/>
```
### Change the form backend class to accept the file
some imports
```
import org.springframework.cloud.gcp.core.GcpProjectIdProvider; import org.springframework.web.multipart.MultipartFile; import org.springframework.context.ApplicationContext; import org.springframework.core.io.Resource; import org.springframework.core.io.WritableResource; import org.springframework.util.StreamUtils; import java.io.*;
```

To accept a file the post method now is defnied as 
```
public String post(
@RequestParam(name="file", required=false) MultipartFile file,
 @RequestParam String name,
 @RequestParam String message, Model model)
throws IOException {

```

We now add the code to retrieve the file and push it to the bucket
```
String filename = null;
if (file != null && !file.isEmpty()
    && file.getContentType().equals("image/jpeg")) {
	// Bucket ID is our Project ID
	String bucket = "gs://" +
	/*      projectIdProvider.getProjectId(); */
	/* instead we use a random string */
	 "test_some_random_name";
	// Generate a random file name
	filename = UUID.randomUUID().toString() + ".jpg";
	WritableResource resource = (WritableResource)
	      context.getResource(bucket + "/" + filename);
	// Write the file to Cloud Storage
	try (OutputStream os = resource.getOutputStream()) {
	     os.write(file.getBytes());
	 }
}

```

Some application logic. We need to keep track of what file belongs to whom thus have to save some data hence some code below 

```
``


-      
-   Modify the HTML template of the frontend application to enable file uploads
    
-   Modify the frontend application to process and store images on Cloud Storage
    
-   Modify the frontend application to display uploaded message images
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyODM1NDM4NCwtMTgxMzQ1NzE2OV19
-->