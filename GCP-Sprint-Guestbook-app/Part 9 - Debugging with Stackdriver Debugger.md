# Using the GCP Cloud debugger
Cloud Debugger is a feature of Google Cloud Platform (GCP) that enables you to inspect the state of an application at any code location, without stopping or slowing down the running app. Cloud Debugger makes it easier to view the application state without adding logging statements.

You can use Cloud Debugger with any deployment of your application, including test, development, and production. Cloud Debugger adds less than 10 milliseconds to the request latency only when the application state is captured. In most cases, this additional latency is not noticeable by users.

Run the frontend application. The results were as below 
There was couple of settings that were missing, that was done and the following is the output
![Build Success](https://i.imgur.com/r4PDWCf.png)

Next we find the URL
`gcloud app browse`

The app link 
![Front end app link](https://i.imgur.com/bFCUL3T.png)

Launch a web browser from the shell and load the front end application
![The frontend app](https://i.imgur.com/acb3YE3.png)

### Examine the cloud logs
This is found in the Logging > Logs Viewer
![Logs](https://i.imgur.com/oeORLPn.png)
### Configure the cloud debugger
Navigate to debugger, select the application, select the source code
![Cloud debugger](https://i.imgur.com/q7SXzM8.png)

### Creating the Source Code Capture
This is done below 
![Source code capture](https://i.imgur.com/ASrNkFB.png)


W
### Configure Cloud Debugger logpoints and snapshots
    
### Enable Cloud Monitoring
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0MDY3NjExOCwtMTc4MjYwNDUxMiwtMT
Y3Nzg1ODQ4OCwtOTQ2NTU0Mjg3LDE1NjUyOTUzOCwxNzE0NjI2
Mzg4LDMxNDEwMTY0NSwtMjA4ODc0NjYxMl19
-->