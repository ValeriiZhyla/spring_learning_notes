_@Document_ annotation defines a name of persisting object in MongoDB.

Let's create a model object, that represents a User with credentials.

```java
@Document("user")
public class User {
    @Id
    private String username;
    private String password;
    private String role;

    public User(String id, String username, String password, String role) {
        this.username = username;
        this.password = password;
        this.role = role;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getRole() {
        return role;
    }

    public void setRole(String role) {
        this.role = role;
    }
}
```

We can use a special repository interface type, the **MongoRepository** to get users from database.

```java
public interface UserRepository extends MongoRepository<User, String> {

    @Query("{name:'?0'}")
    User findUserByUsername(String username);
}

```

More about [[MongoRepository]].