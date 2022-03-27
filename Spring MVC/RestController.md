@RestController annotation in just a combination of the @Controller and the @ResponseBody

```java
@RestController
public class HelloController {
    
    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String sayHello() {
        return "Hello";
    }
}
```


We can return different object types and data structures from controller, not only the strings. Objects will be transformed internally to jsons.

```java
@RestController
public class BooksController {

	@RequestMapping(value = "/book", method = RequestMethod.GET)
    public Book getOneBook() {
        return new Book(0, "AABB", "A0");
    }

    @RequestMapping(value = "/books", method = RequestMethod.GET)
    public List<Book> getAllBooks() {
	    List<Book> books = Arrays.asList(new Book(1111, "AAAA", "A1"), new Book(2222, "BBBB", "A2"));
        return books;
    }
}
```

I'll use Postman to test the endpoints. The endpoint _/books_ returns a Json Array.

```json
[{"id":1111,"title":"AAAA","author":"A1"},{"id":2222,"title":"BBBB","author":"A2"}]
```


Links:
- https://www.youtube.com/watch?v=oRFCeRVWCNE&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=11
- https://www.youtube.com/watch?v=gDHSLKmG8ZQ&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=12