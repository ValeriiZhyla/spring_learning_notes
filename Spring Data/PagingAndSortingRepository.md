An inteface PagingAndSortingRepository extends the interface [[CRUD Repository]].

Documentation: https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html

Usage: https://www.baeldung.com/spring-data-jpa-pagination-sorting

If we extend an interface PagingAndSortingRepository, we can use two new features - pagination and sorting.

Pageable javadoc: https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/domain/Pageable.html

Let's define a reference repository:
```java
public interface ProductRepository extends PagingAndSortingRepository<Product, Integer> {

    List<Product> findAll(Sort sort);
    
	List<Product> findAllByPrice(double price, Sort sort);

	List<Product> findAllByPrice(double price, Pageable pageable);
}
```

## Sorting
Sort object is an object that represents the sorting relation, that can be applied to data.

This sort object can be applied to query, to get the object list sorted by descending order by column "price".
```java
Sort sortPriceDesc = Sort.by(Sort.Direction.ASC, "price");
List<Product> productsSortedByPrice = repository.findAll(sortPriceDesc);
```


## Paging