We can bind native MongoDB queries to repository methods with _@Query_ Annotation.

Guide: https://javatechonline.com/spring-boot-mongodb-query-examples/

_@Query_ takes a JSON string as argument. 

Let's assume, that out MongoDB instance stores Book objects with fields:
- int id (Primary Key)
- String title
- int price
- int pages  

The parameters will be injected in query, positions can be marked with ?0 for first parameter, ?1 for second parameter, ?2 for third etc. 

Note, that String parameters have to be wrapped with quotes.

```java
public interface BookRepository extends MongoRepository<Book, Integer> {

	@Query("{id:?0}")
    Book findBookById(int id);

    @Query("{title:'?0'}")
    Book findBookByTitle(String title);
    
}

```

## Syntax

Here is an overview for query syntax
![[MongoDB_Queries_Table.png]]

And the comparison to classical SQL Statements

![[MongoDB_Queries.webp]]

## Operators

Note, that the mathematical and logical operators like <, >, not are presented as named functions: $lt, $gt, $ne.

```java
public interface BookRepository extends MongoRepository<Book, Integer> {

	@Query("{price: {$lt: ?0}}")
    List<Book> findAllBooksCheaperThan(int upperPriceBorder);

	@Query("{pages: {$gt: ?0, $lt : ?1}}")
    List<Book> findAllBooksWithPagesBetween(int minPages, int maxPages);
    
}

```

## Projection
We can project the result with the fields parameter. 

Expression fields="{a:1}" defines, that only field a should be displayed (and all others are implicit marked with fieldname:0)

```java
public interface BookRepository extends MongoRepository<Book, Integer> {

	@Query("{price: {$lt: ?0}}")
    List<Book> findAllBooksCheaperThan(int upperPriceBorder);

	@Query(value = "{pages: {$gt: ?0, $lt : ?1}}",
		   fields = "{price:1, pages:1}")
    List<Book> findAllPricesOfBooksWithPagesBetween(int minPages, int maxPages);
    
}

```

