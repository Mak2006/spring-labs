Google Cloud Platform (GCP) offers many other APIs that you can use directly from your Java applications.  In this lab, we integrate our Spring applications with GCP API's, in particular, use Cloud Vision API to analyze the images uploaded by the users.

Vision API enables developers to understand the content of an image by encapsulating powerful machine-learning models in an easy-to-use REST API. Vision API quickly classifies images into thousands of categories, detects individual objects and faces within images, and reads printed words contained in images. You can build metadata on your image catalog, moderate offensive content, or enable new marketing scenarios through image sentiment analysis. Vision API enables your applications to easily detect broad sets of objects in your images, from flowers, animals, or transportation to thousands of other object categories commonly found in images.

### Add a GCP API Java library to an application
Enable the API's
`gcloud services enable vision.googleapis.com`

Add the dependency to the application 
```
<dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>google-cloud-vision</artifactId>
</dependency>

```
### Create a GCP credential scope for Spring
Add the GCP scope to the application properties
`spring.cloud.gcp.credentials.scopes=https://www.googleapis.com/auth/cloud-platform`

### Create a Java bean that implements Vision API features
We would add this where the Spring is initialised say the app context. 
```
import java.io.IOException; import com.google.cloud.vision.v1.*; import com.google.api.gax.core.CredentialsProvider;
```
Adding the bean
```
// This configures the Vision API settings with a
// credential using the the scope we specified in
// the application.properties.
@Bean
public ImageAnnotatorSettings imageAnnotatorSettings(
	CredentialsProvider credentialsProvider)
	throws IOException {
	return ImageAnnotatorSettings.newBuilder()
	.setCredentialsProvider(credentialsProvider).build();
}

@Bean
public ImageAnnotatorClient imageAnnotatorClient(
	ImageAnnotatorSettings settings)
	throws IOException {
   return ImageAnnotatorClient.create(settings);
}

```

### Use Vision API to add image analysis to an application
To the microservice where we want to analyse the image we do the following. This would be the app where we did the initialization steps above. 

```
import com.google.cloud.vision.v1.*;

// Analysing the data

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTM5NTMzNDc3LDczMDk5ODExNl19
-->