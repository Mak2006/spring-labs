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

### Create service accounts to use the API
We would require further a service account for our application to use the API
```
gcloud iam service-accounts create guestbook
// Assigning a editor account, in prod, consider a reduced perm set
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member serviceAccount:guestbook@${PROJECT_ID}.iam.gserviceaccount.com --role roles/editor

//Generate a JSON key to be used by the app to use for accessing this 
//This command creates service account credentials that are stored in the `$HOME/service-account.json` file.
gcloud iam service-accounts keys create \ ~/service-account.json \ --iam-account guestbook@${PROJECT_ID}.iam.gserviceaccount.com
```

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
@Autowired
private ImageAnnotatorClient annotatorClient;

private void analyzeImage(String uri) {
// After the image was written to GCS,
// analyze it with the GCS URI.It's also
// possible to analyze an image embedded in
// the request as a Base64 encoded payload.
List<AnnotateImageRequest> requests = new ArrayList<>();
ImageSource imgSrc = ImageSource.newBuilder()
     .setGcsImageUri(uri).build();
Image img = Image.newBuilder().setSource(imgSrc).build();
Feature feature = Feature.newBuilder()
     .setType(Feature.Type.LABEL_DETECTION).build();
AnnotateImageRequest request = AnnotateImageRequest
     .newBuilder()
     .addFeatures(feature)
     .setImage(img)
     .build();
requests.add(request);
BatchAnnotateImagesResponse responses =
      annotatorClient.batchAnnotateImages(requests);
   // We send in one image, expecting just
   // one response in batch
AnnotateImageResponse response =responses.getResponses(0);
System.out.println(response);
}

```

### Test the application
Run the app.  Upload some images and check the caterogy of the image in the log. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAzMjc1MDQxMSwtMjAzNzMzNDUyNyw3Mz
A5OTgxMTZdfQ==
-->