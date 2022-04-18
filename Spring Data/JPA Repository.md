Interface JpaRepository is the most powerful interface in Spring Data JPA.
It contains the functionality from [[CRUD Repository]] and [[PagingAndSortingRepository]], and introduces some new features.

Documentation: https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html

## Explicit Queries with @Query

With _@Query_ annotation we can specify the exact SQL Statements

```java
public interface UserRepository extends JpaRepository<User, Long> {

  @Query("select u from User u where u.firstname = :firstname or u.lastname = :lastname")
  User findByLastnameOrFirstname(@Param("lastname") String lastname,
                                 @Param("firstname") String firstname);
}
```