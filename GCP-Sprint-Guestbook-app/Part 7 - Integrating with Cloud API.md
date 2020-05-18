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
### Create a Java bean that implements Vision API features
### Use Vision API to add image analysis to an application
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3NDMyNTYxNyw3MzA5OTgxMTZdfQ==
-->