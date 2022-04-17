I'll use create a PostgreSQL instance on Heroku and use it for connection.
I is important to allow access to the cloud instance from your ip address.

Guide: https://www.codejava.net/frameworks/spring-boot/connect-to-postgresql-database-examples

We have to specify following parameters in application.properties:

```properties
spring.datasource.url=
spring.datasource.username=
spring.datasource.password=
spring.datasource.driver-class-name=org.postgresql.Driver
```

Note, that the dependency spring-boot-starter-data-jpa and postgres driver is required.
```xml
<dependency>  
   <groupId>org.springframework.boot</groupId>  
   <artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>

<dependency>  
   <groupId>org.postgresql</groupId>  
   <artifactId>postgresql</artifactId>  
</dependency>
```

My credentials:

```properties
spring.datasource.url=jdbc:postgresql://ec2-52-18-116-67.eu-west-1.compute.amazonaws.com:5432/dbmiq3db65kq18
spring.datasource.username=rtqdhjzpirhsbt
spring.datasource.password=***********************************************
```

Usually i use the Datagrip (or free Dbeaver) to establish the initial database connection and the form the connection url.

If you are getting errors on Spring startup, then try to connect via some database IDE at first, it would give you some detailed problem specification.