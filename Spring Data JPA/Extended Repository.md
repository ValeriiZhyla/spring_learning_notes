Let's make our entity a little bit more complex, by adding the GrapeSort field to Wine class.

```java
@Entity  
public class GrapeSort {  
    @Id  
 private String name;  
}
```

If we link one entity with another entity, we have to define the cardinality of relation: [[JPA Relations]]


One Wine can have only one sort (naive assumption), but there can be different wines, that use the same grape sort.

Structure is "MainClass-to-Field". Many Wine types to one GrapeSort Therefore in this case we have to use @ManyToOne relation.

```java
@Entity  
public class Wine {  
  
    @Id  
 private String id;  
 private String name;  
 private String producer;  
  
 @ManyToOne  
 private GrapeSort grapeSort;
```

If we want to get the list of wines of one specific GrapeSort, we can't just use the [[CRUD Repository]].
In this case, we have to define a new method in the interface. If we use the correct method name, JPA will generate the code from it, without any additional annotation.

```java
public interface WineRepository extends CrudRepository<Wine, String> {  
    public List<Wine> findAllByGrapeSortName(String grapeSortName);  
}
```

Stucture: find\[All\]By{Entity}{Field}

More rules here: https://www.baeldung.com/spring-data-derived-queries