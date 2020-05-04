# Boot Postgre App

1. Simple app to use spring Initializer to creat Spring boot application with Postgre backend
	1. Java 11, Postgre, Spring Web, Spring Boot, Maven, 
2. **Creating a boot using Initializer -**  Two ways of going, either you can use the IDE plugins or use Spring Initializer
	1. Head over to [https://start.spring.io/](https://start.spring.io/), select the bits, Java, Spring boot version, select Jar package and choose the dependencies, we use Spring-Web, Thymeleaf and download the zip.  
	2. Unzip and use maven import of the project. 
	3. This is more easily done using IDE Plugin. 
3. Get to the src and launch the application. Point browser to 
localhost:8080/ we shall see this. 

![enter image description here](https://i.imgur.com/rmaQeHP.png)

4. Take aways, 
	 1. The @SpringBootApplication is the trigger for Spring Boot Autoconfiguration. This is the application file. Corresponding to this a test file is also generated. 
	 2. pom.xml  and application.properties are also present. 
6. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ3NzM3MzY3OSw1ODU2Nzg2MzQsLTUwNz
kwODMzMCwtMTI4NDgyNTU0OCwxMjg3ODkzMzk5LC03NDA3ODk1
OTcsLTE0MjQxMDY0ODcsLTE0NjM3MzI5ODksNzczOTI0NjIzLD
IwNTU2OTc2NTJdfQ==
-->