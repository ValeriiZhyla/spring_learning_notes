We can create a controller for REST API with @RestController annotation. It is just a combination of the @Controller and the @ResponseBody annotations.

```java
@RestController
public class HelloController {
    
    @RequestMapping(method = RequestMethod.GET, value = "/hello")
    public String sayHello() {
        return "Hello";
    }
}
```

Controllers are using Servlets intermally: [[Servlets and Controllers]]

## GET Endpoints

We can return different object types and data structures from controller, not only the strings. Objects will be transformed internally to jsons.

```java
@RestController
public class BookController {
    private final BookService bookService;

    @Autowired
    public BookController(BookService bookService) {
        this.bookService = bookService;
    }

    @RequestMapping(method = RequestMethod.GET, value = "/books")
    public List<Book> getAllBooks() {
        return bookService.getAllBooks();
    }
    
    @RequestMapping(method = RequestMethod.GET, value = "/books/{id}")
    public Book getBookById(@PathVariable("id") Long id) {
        return bookService.getBookById(id);
    }
}
```

The Service BookService is described here: [[Service]]

I'll use Postman to test the endpoints. The endpoint _/books_ returns a Json Array.
GET http://localhost:8080/books ->

```json
[
 {
 "id": 145,
 "title": "Spring",
 "author": "Baeldung"
 },
 {
 "id": 932,
 "title": "Operating Systems",
 "author": "Tanenbaum"
 },
 {
 "id": 12,
 "title": "Clean Code",
 "author": "Uncle Bob"
 }
]
```

Links:
- https://www.youtube.com/watch?v=oRFCeRVWCNE&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=11
- https://www.youtube.com/watch?v=gDHSLKmG8ZQ&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=12
- 
#### Variables Mapping
```java
@RestController
public class BookController {
    private final BookService bookService;

    @Autowired
    public BookController(BookService bookService) {
        this.bookService = bookService;
    }

    @RequestMapping(method = RequestMethod.GET, value = "/books")
    public List<Book> getAllBooks() {
        return bookService.getAllBooks();
    }
    
    @RequestMapping( method = RequestMethod.GET, value = "/books/{id}")
    public Book getBookById(@PathVariable("id") Long id) {
        return bookService.getBookById(id);
    }
}
```

We can define our variable position in URL, and use annotation @PathVariable to connect it with java parameter.

We can omit the name parameter of @PathVariable, if the variable name corresponds with name in URL. Long id and {id}.

```java
    @RequestMapping(method = RequestMethod.GET, value = "/books/{id}")
    public Book getBookById(@PathVariable Long id) {
        return bookService.getBookById(id);
    }

```

But if the names are different, we have to define the name:
```java
    @RequestMapping(method = RequestMethod.GET, value = "/books/{id}")
    public Book getBookById(@PathVariable("id") Long identifier) {
        return bookService.getBookById(identifier);
    }

```

Type will be converted automatically. If type is incorrect, server will send Bad Request Error. 

Get http://localhost:8080/books/12 ->
```json
{
 "id": 12,
 "title": "Clean Code",
 "author": "Uncle Bob"
}
```

Links: 
- https://www.youtube.com/watch?v=AI2oBJkPK3c&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=18


## POST Endpoints
We have to set the RequestMethod, and use the _@RequestBody_ annotation. _@RequestBody_ marks, that Http Body contains a JSON, that should be mapped to the Book object.

```java
@RequestMapping(method = RequestMethod.POST, value = "/books")  
public void addNewBook(@RequestBody Book book) {  
    bookService.addBook(book);  
}
```

Links:
- https://www.youtube.com/watch?v=AI2oBJkPK3c&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=19

## PUT Endpoints
Like Post Endpoint, but requires some additional key (depends on business logic) and PUT parameter.

```java
@RequestMapping(method = RequestMethod.PUT, value = "/books/{id}")  
public void addNewBook(@RequestBody Book book, @PathVariable Long id) {  
    bookService.updateBookWithExistingId(book, id);  
}
```

Links:
- https://www.youtube.com/watch?v=AI2oBJkPK3c&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=20


## DELETE Endpoints
Requires DELETE parameter.
```java
@RequestMapping(method = RequestMethod.DELETE, value = "/books/{id}")  
public void addNewBook(@PathVariable Long id) {  
    bookService.deleteBookById(id);  
}
```

Links:
- https://www.youtube.com/watch?v=AI2oBJkPK3c&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=20

