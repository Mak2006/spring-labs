# Boot Postgre App

1. Simple app to use spring Initializer to creat Spring boot application with Postgre backend
	1. Java 11, 
	2. Database - H2 and Postgre on Docker,
	3. Spring framework - Spring Web, Spring Boot, Spring Data 
	4. Build - Maven, 
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
5. At this point we will bring in a db.  For this we create a mock schema and some data. We use [Generatedata.com](Generatedata.com) for this purpose.  We generate a ddl and data.  

![enter image description here](https://i.imgur.com/YeHcNx7.png)

(There are two hacks that we have to do to make this compatible with H2, that is replace " with ' on the data and omit the `.)

6. We now create a H2Database and use JPA to connect to it. To get Spring to include this we change the pom to include H2 and JPA dependency.  We include the following 
```
<dependency>  
   <groupId>org.springframework.boot</groupId>  
   <artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>  
<dependency>  
   <groupId>com.h2database</groupId>  
   <artifactId>h2</artifactId>  
</dependency>
```
7.  We further set two properties 
```
spring.jpa.hibernate.ddl-auto=none
logging.level.org.springframework.jdbc.datasource.init.ScriptUtils=debug
```
9. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzM0MzYyNDY0LDUwNTM1ODUxMCw0NDY4Nz
c2NjIsLTIzNDA2MjEwNywtMTE5ODMwNzU5MiwtMTcxNjUwOTQ2
MSwtNTY1MjM1NjAwLDU4NTY3ODYzNCwtNTA3OTA4MzMwLC0xMj
g0ODI1NTQ4LDEyODc4OTMzOTksLTc0MDc4OTU5NywtMTQyNDEw
NjQ4NywtMTQ2MzczMjk4OSw3NzM5MjQ2MjMsMjA1NTY5NzY1Ml
19
-->