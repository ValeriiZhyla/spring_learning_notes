Instead of getting a users directly from the _DataSource_ we can add one more abstraction level, and use the _UserDetailsService_.

The usage of _DataSource_ is described here: [[Configuring the Users with DataSource]].

## Hardcoded user
Let's add an instance, that implements an _UserDetailsService_ interface.

```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    private final UserDetailsService userDetailsService;

    @Autowired
    public SecurityConfiguration(HardcodedUserDetailsService userDetailsService) {
        this.userDetailsService = userDetailsService;
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService);
    }
}
```

The purpose of _UserDetailsService_ - get the userName and return an object that implements an _UserDetails_ interface. It can be some hardcoded user, it can be retrieved from a database JDBC directly or with JPA indirectly, it can be read from some textfile etc. It has to be implemented, and it is fully generic abstraction.

In this example we will simply return a user with password "password" and role "ROLE_USER" for all userNames;

```java
@Service
public class HardcodedUserDetailsService implements UserDetailsService {

    @Override
    public UserDetails loadUserByUsername(String userName) throws UsernameNotFoundException {
        return new HardcodedUserDetails(userName);
    }
}
```

We have to implement a bunch of methods to implement the interface _UserDetails_


```java
public class HardcodedUserDetails implements UserDetails {
    private final String userName;

    public HardcodedUserDetails(String userName) {
        this.userName = userName;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return Arrays.asList(new SimpleGrantedAuthority("ROLE_USER"));
    }

    @Override
    public String getPassword() {
        return "password";
    }

    @Override
    public String getUsername() {
        return userName;
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}
```

## Accessing the External Database with JPA
Let's assume, that we have configuted some external database with table _users_, where each user has some id, username, password, active state and roles.

Connecting to External Database: [[Set up the Database Connection]]

We have to define the user JPA Entity:

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private int id;
    private String username;
    private String password;
    private boolean active;
    private String roles;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String userName) {
        this.username = userName;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public boolean isActive() {
        return active;
    }

    public void setActive(boolean active) {
        this.active = active;
    }

    public String getRoles() {
        return roles;
    }

    public void setRoles(String roles) {
        this.roles = roles;
    }
}

```

And a repository, to get the users by name:

```java

```