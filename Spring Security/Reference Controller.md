## Simple Controller
```java
@RestController
public class HomeResource {

    @GetMapping("/")
    public String home() {
        return "Welcome";
    }

    @GetMapping("/user")
    public String homeUser() {
        return "Welcome User";
    }

    @GetMapping("/admin")
    public String homeAdmin() {
        return "Welcome Admin";
    }
}
```