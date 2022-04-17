Documentation: 

We have to create an interface for database connection. If we want simple CRUD operations, then we can extend class CrudRepository<Class, PrimaryKeyType>.

Only create an interface, and extend the class. No further code. Not a joke.
```java
public interface WineRepository extends CrudRepository<Wine, String> {  
}
```

Then we have to autowire this repository to our service and use it.

```java
@Service  
public class WineService {  
    private final WineRepository wineRepository;  
  
 @Autowired  
 public WineService(WineRepository wineRepository) {  
        this.wineRepository = wineRepository;  
 }  
  
    public List<Wine> getAllWines() {  
        List<Wine> wines = new ArrayList<>();  
 wineRepository.findAll().forEach(wines::add);  
 return wines;  
 }  
  
    public void addWine(Wine wine) {  
        wineRepository.save(wine);  
 }  
  
    public Wine getWineById(String id) {  
        return wineRepository.findById(id).get();  
 }  
}
```

Important methods:
- findAll()
- findById(id)
- findAllById(id)
- save(obj)
- saveAll(list)
- delete(obj)
- deleteById(id)
- deleteAll()
- deleteAll(list)

The class representing the model are described in [[Entity]].

The repository with custom methods is described here: [[Repository Usage]]

Links: 
- https://www.youtube.com/watch?v=z3HnFBzn7DI&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=28
- https://www.youtube.com/watch?v=lpcOSXWPXTk&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=29