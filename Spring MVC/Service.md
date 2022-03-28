We can mark the class that manages some business logic with @Service annotation.

```java
@Service
public class BookService {
    List<Book> books;

    public BookService() {
        this.books = new ArrayList<>();
        books.add(new Book(145, "Spring", "Baeldung"));
        books.add(new Book(932, "Operating Systems", "Tanenbaum"));
    }

    public List<Book> getAllBooks() {
        return books;
    }

    public Book getBookById(Long id) {
        return books.stream().filter(b -> b.getId().equals(id)).findFirst().get();
    }
}
```

And then autowire it the controller class.

```java
@RestController
public class BookController {
    private final BookService bookService;

    @Autowired
    public BookController(BookService bookService) {
        this.bookService = bookService;
    }

    @RequestMapping(value = "/books", method = RequestMethod.GET)
    public List<Book> getAllBooks() {
        return bookService.getAllBooks();
    }
}
```