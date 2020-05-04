# Boot Postgre App

1. Simple app to use spring Initializer to creat Spring boot application with Postgre backend
	1. Java 11, Postgre on Docker, Spring Web, Spring Boot, Maven, 
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
5. At this point we will bring in a db.  For this we create a mock schema and some data. We use [https://mockaroo.com/](https://mockaroo.com/) for this purpose.  We generate a ddl and data.  


7. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1NTEyNDYwNywtMTcxNjUwOTQ2MSwtNT
Y1MjM1NjAwLDU4NTY3ODYzNCwtNTA3OTA4MzMwLC0xMjg0ODI1
NTQ4LDEyODc4OTMzOTksLTc0MDc4OTU5NywtMTQyNDEwNjQ4Ny
wtMTQ2MzczMjk4OSw3NzM5MjQ2MjMsMjA1NTY5NzY1Ml19
-->