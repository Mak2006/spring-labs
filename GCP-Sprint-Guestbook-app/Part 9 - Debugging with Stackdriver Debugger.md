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


We are now in a position to use the debugger . The source code capture now appears in the debugger
![Source code capture](https://i.imgur.com/nvbPZx5.png)

### Configure Cloud Debugger logpoints and snapshots
We can now add tons of log as much we want to. At this point we say we want to investigate why the files uploaded are not being shown. For this we set a log point as below 
![enter image description here](https://i.imgur.com/Lmd2q5s.png)
   
Note - a log has a validity period ! .  This is a nice feature. 
### Enable Cloud Monitoring
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTA4MDEwNTI1LC0xMzA1MTIxNTM1LC0xNz
gyNjA0NTEyLC0xNjc3ODU4NDg4LC05NDY1NTQyODcsMTU2NTI5
NTM4LDE3MTQ2MjYzODgsMzE0MTAxNjQ1LC0yMDg4NzQ2NjEyXX
0=
-->