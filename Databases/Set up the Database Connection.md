## Creating a MongoDB instance

At first, i'll use a free MongoDB Atlas instance: https://www.mongodb.com/docs/atlas/getting-started/

I'll create the database sandbox with username admin and password admin_password.
My connection URL: 

```url
mongodb+srv://admin:admin_password@sandboxcluster.ngis0.mongodb.net/sandbox?retryWrites=true&w=majority
```


## Connecting to MongoDB 
Guide about connecting Spring Boot to MongoDB Atlas: https://www.mongodb.com/compatibility/spring-boot

We have to add a Spring Boot MongoDB Dependency (spring-boot-starter-data-mongodb in Maven)

These two properties will be set in application.properties to configure the URL, username and password. 
**This is a sandbox example, do not store the passwords in configs in real life! Use some environment variables and secrets instead**

```properties

spring.data.mongodb.uri=mongodb+srv://<username>:<pwd>@<cluster>.mongodb.net/databasename

spring.data.mongodb.database=databasename
```

My properties:

```properties

spring.data.mongodb.uri=mongodb+srv://admin:admin_password@sandboxcluster.ngis0.mongodb.net/sandbox

spring.data.mongodb.database=sandbox
```

If specified database does not exist, MongoDB will create a new one.

Then we have to specify, that we want a connection with MongoDB. It can be done with just one annotation _@EnableMongoRepositories_ in main apllication file

```java
@SpringBootApplication
@EnableMongoRepositories

public class SecurityJdbcApplication {

	public static void main(String[] args) {
		SpringApplication.run(SecurityJdbcApplication.class, args);
	}

}
```

## Database IDE
I'll use DataGrip to view and manipulate the database. There are also good free alternatives, my personal open-souce favourite is DBeaver.