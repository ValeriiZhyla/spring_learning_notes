An inteface PagingAndSortingRepository extends the interface [[CRUD Repository]].

Documentation: https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html

Usage: https://www.baeldung.com/spring-data-jpa-pagination-sorting

If we extend an interface PagingAndSortingRepository, we can use two new features - pagination and sorting.

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
Sort sortPriceDesc = Sort.by(Sort.Direction.DESC, "price");
List<Product> productsSortedByPrice = repository.findAll(sortPriceDesc);
```

or, alternatively:

```java
Sort sortPriceDesc = Sort.by("price").descending();
List<Product> productsSortedByPrice = repository.findAll(sortPriceDesc);
```

We can also chain different sorts:

```java
Sort sortPriceDesc = Sort.by("price").descending().and(Sort.by("name"));
List<Product> productsSortedByPrice = repository.findAll(sortPriceDesc);
```

## Paging
Paging (or pagination) is helpful, when we have a large dataset and we want to present it in smaller chunks, called pages.

To use it, we have to create a PageRequest object, which defines, which pages we want to get and how many object should this page contain.

**The action, that is achieved with paging, is aquivalent to "WHERE ROWNUM <= 5" in Oracle or "LIMIT 5" in PostgreSQL**

```java
Pageable firstPageWithFiveElements = PageRequest.of(0, 5);

Page<Product> allProductsFirstPage = repository.findAll(firstPageWithTwoElements);

```

We can return Page object or List object from findAll* method. Page is a list, that also knows about hte total number of available pages.

## Paging and Sorting
We can also use paging and sorting together. For example, if we want the five products with the highest price, we can use following code:

```java
Pageable sortedByPriceDescTopFive = 
	PageRequest.of(0, 5, Sort.by("price").descending());

List<Product> topExpensiveProducts = 
findAll(sortedByPriceDescTopFive);
```


Pageable javadoc: https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/domain/Pageable.html

PageRequest javadoc: https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/domain/PageRequest.html