# Using the GCP Cloud debugger
This series is a 12 part series in creating Spring application with GCP services. These are the notes that was created as part of coursework for the course titled Building Scalable Java Microservices with Spring Boot and Spring Cloud!

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

### Check the logs now 
![Logging](https://i.imgur.com/v9T88Gb.png)
The new logs are in blue. 

We find our log 
![Log](https://i.imgur.com/kRHdSoJ.png)

this tells us the application is indeed receiving the file.  A bad example however, it helps, in this case it is evident that the application accepts only jpeg and we are uploading a png. 
We upload a jpeg. 
We can see our image this time  - 
![Screw driver](https://i.imgur.com/RO4juLF.png)

### Enable Cloud Monitoring
Go to monitoring, wait for it to finish
![Monitoring provisioning](https://i.imgur.com/szg09Bf.png)

We can see extensive monitoring now, those that are enabled by default.
![Monitoring](https://i.imgur.com/LOwCjNX.png)
That completes the lab. 
 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2NzYyMjAwLC0yMDQ1MDAzMDk0LC0xMD
EyNzc5MjQsLTEzMDUxMjE1MzUsLTE3ODI2MDQ1MTIsLTE2Nzc4
NTg0ODgsLTk0NjU1NDI4NywxNTY1Mjk1MzgsMTcxNDYyNjM4OC
wzMTQxMDE2NDUsLTIwODg3NDY2MTJdfQ==
-->