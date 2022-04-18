Interface JpaRepository is the most powerful interface in Spring Data JPA.
It contains the functionality from [[CRUD Repository]] and [[PagingAndSortingRepository]], and introduces some new features.

Documentation: https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html

Important are batch and flush methods, that can modify many entities in a single transaction.

## Explicit Queries with @Query

With _@Query_ annotation we can specify the exact SQL Statements. We can also use the named arguments, with usage of _@Param_ annotation.

```java
public interface UserRepository extends JpaRepository<User, Long> {

  @Query("SELECT u FROM User u WHERE u.firstname = :firstname OR u.lastname = :lastname")
  User findByLastnameOrFirstname(@Param("lastname") String lastname,
                                 @Param("firstname") String firstname);
}
```

More about queries and parameter naming: https://docs.spring.io/spring-data/data-jpa/docs/current/reference/html/#jpa.named-parameters