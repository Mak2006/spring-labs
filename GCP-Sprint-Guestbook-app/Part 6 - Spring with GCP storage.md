Google Cloud Platform (GPC) has a bucket-based object storage solution called Cloud Storage. Cloud Storage is designed to store a large number of files and a large volume of binary data, so that you don't need to manage your own file systems or file sharing services. Cloud Storage can be used directly by many other GPC products. For example, you can store data files on Cloud Storage and process those data filesin a managed Hadoop (Cloud Dataproc) cluster. You can also import structured data stored on Cloud Storage directly into BigQuery for ad hoc data analytics using standard SQL.

Cloud Storage provides fast, low-cost, highly durable, global object storage for developers and enterprises that need to manage unstructured file data. In Cloud Storage, the consistent API, low latency, and speed across storage classes simplify development integration and reduce code complexity.

In this lab, you add the ability to upload an image associated with a message. You store the image in Cloud Storage.

### Add the Spring starter for Cloud Storage
We do this in the appliation that requires cloud storage. In
-   Create a Cloud Storage bucket
    
-   Modify the HTML template of the frontend application to enable file uploads
    
-   Modify the frontend application to process and store images on Cloud Storage
    
-   Modify the frontend application to display uploaded message images
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM2MjEzMTUxN119
-->