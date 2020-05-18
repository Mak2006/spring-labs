# Deploying application to Google App Engine
App Engine is Google's fully managed serverless application platform. With App Engine, you can build and deploy applications on a fully managed platform and scale your applications without having to worry about managing the underlying infrastructure. App Engine includes capabilities such as automatic scaling-up and scaling-down of your application, and fully managed patching and management of your servers.

In this lab, you deploy the application into App Engine. You need to convert the application from fat WARs into the thin-WAR deployments that App Engine can deploy.

### Initialize App Engine
Enable app
`gcloud app create --region=us-central`

Add the App engine as a plugin to application
```
<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>appengine-maven-plugin</artifactId>
  <version>1.3.1</version>
  <configuration>
	<version>1</version>
  </configuration>
</plugin>

```
Add a `appengine-web.xml` to your application in the `WEB-INF` directory of the application.  Note in prod scenario you may use auto scaling. 
```
<appengine-web-app xmlns="http://appengine.google.com/ns/1.0">
  <service>default</service>
  <version>1</version>
  <threadsafe>true</threadsafe>
  <runtime>java8</runtime>
  <instance-class>B4_1G</instance-class>
  <sessions-enabled>true</sessions-enabled>
  <manual-scaling>
    <instances>2</instances>
  </manual-scaling>
  <system-properties>
    <property name="spring.profiles.active" value="cloud" />
  </system-properties>
</appengine-web-app>
```


### Reconfigure an application to work with App Engine
    
### Configure the Cloud Runtime Runtime Configuration API to automatically provide the backend URL to the Frontend application
    
### Deploy the application to App Engine
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUxNTMzNTA3NCwxMjYyNTcyMTUyLC0yMD
g4NzQ2NjEyLDczMDk5ODExNl19
-->