We can use a special repository interface type, the **MongoRepository** to get users from database. 

```java
public interface UserRepository extends MongoRepository<User, String> {
	
    User findUserByUsername(String username);
    
}
```

The implementation of the function will be automatically derived from it's name. The patterns of function naming are described here: https://www.baeldung.com/spring-data-derived-queries

We can also define the query explicitely with _@Query_ annotations. This way is more robust and suitable for complex queries.

```java
public interface UserRepository extends MongoRepository<User, String> {

    @Query("{name:'?0'}")
    User findUserByUsername(String username);
    
}
```

More about [[MongoDB Queries]].

Documentation: https://docs.spring.io/spring-data/mongodb/docs/current/api/org/springframework/data/mongodb/repository/MongoRepository.html