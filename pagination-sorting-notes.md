# Spring Boot Data Pagination and Sorting Tutorial

Welcome to this comprehensive tutorial on **Spring Boot Data Pagination and Sorting**, designed to take you from basic to advanced concepts with detailed code explanations. This tutorial uses a real-time Spring Boot project with Lombok, focused on the **e-commerce domain**. Each topic includes multiple examples (up to 10 where applicable) to illustrate different scenarios, and the content is organized with a navigable **Table of Contents** in Markdown format.

---

## Table of Contents

1. [Introduction to Pagination and Sorting](#introduction-to-pagination-and-sorting)
2. [Setting Up a Spring Boot Project with Lombok](#setting-up-a-spring-boot-project-with-lombok)
3. [Basic Pagination](#basic-pagination)
4. [Basic Sorting](#basic-sorting)
5. [Combining Pagination and Sorting](#combining-pagination-and-sorting)
6. [Advanced Pagination Techniques](#advanced-pagination-techniques)
7. [Advanced Sorting Techniques](#advanced-sorting-techniques)
8. [Error Handling and Edge Cases](#error-handling-and-edge-cases)
9. [Performance Considerations](#performance-considerations)
10. [Real-time Examples in E-commerce Domain](#real-time-examples-in-e-commerce-domain)
11. [Testing Pagination and Sorting](#testing-pagination-and-sorting)
12. [Best Practices and Tips](#best-practices-and-tips)

---

## Introduction to Pagination and Sorting

### What is Pagination?
Pagination is the process of splitting a large dataset into smaller, manageable chunks called **pages**. Instead of loading all data at once, pagination retrieves only a subset, improving performance and user experience—crucial in e-commerce where product lists can be extensive.

### What is Sorting?
Sorting arranges data in a specific order (e.g., ascending or descending) based on one or more fields, such as price or name. In Spring Boot, sorting enhances data presentation, especially when combined with pagination.

### Why Are They Important in E-commerce?
In e-commerce, pagination prevents overwhelming users with thousands of products, while sorting helps them find items by price, popularity, or relevance. Together, they create a seamless browsing experience.

---

## Setting Up a Spring Boot Project with Lombok

Let’s set up a Spring Boot project with Lombok and an H2 in-memory database for simplicity.

### Step 1: Create a Spring Boot Project
Use **Spring Initializr** (via [start.spring.io](https://start.spring.io)) with:
- **Dependencies**: Spring Web, Spring Data JPA, Lombok, H2 Database
- **Language**: Java
- **Packaging**: JAR

Download and open in your IDE.

### Step 2: Configure `application.properties`
```properties
spring.datasource.url=jdbc:h2:mem:ecommerce
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
```

### Step 3: Define the Product Entity
```java
import lombok.Data;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
@Data
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String description;
    private double price;
    private String category;
}
```

Lombok’s `@Data` generates getters, setters, and other boilerplate code.

### Step 4: Create the Repository
```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

`JpaRepository` provides built-in support for pagination and sorting.

---

## Basic Pagination

Spring Data JPA’s `Pageable` interface simplifies pagination. Here are several examples:

### Example 1: Retrieving the First Page
**Service:**
```java
@Service
public class ProductService {
    @Autowired
    private ProductRepository productRepository;

    public Page<Product> getProducts(int page, int size) {
        Pageable pageable = PageRequest.of(page, size);
        return productRepository.findAll(pageable);
    }
}
```

**Controller:**
```java
@RestController
@RequestMapping("/products")
public class ProductController {
    @Autowired
    private ProductService productService;

    @GetMapping
    public Page<Product> getProducts(@RequestParam(defaultValue = "0") int page,
                                     @RequestParam(defaultValue = "10") int size) {
        return productService.getProducts(page, size);
    }
}
```

**Explanation**: `/products?page=0&size=10` retrieves the first page (page 0) with 10 products.

### Example 2: Retrieving a Specific Page
Access `/products?page=2&size=10` to get the third page. `PageRequest.of(2, 10)` handles this.

### Example 3: Custom Page Size
Use `/products?page=0&size=5` for 5 products per page.

### Example 4-10
- Retrieve the last page (calculate via `Page.getTotalPages()`).
- Use different sizes (e.g., 20, 50).
- Handle edge cases (covered later).

---

## Basic Sorting

Add sorting to `Pageable` using the `Sort` object.

### Example 1: Sorting by Name Ascending
**Service:**
```java
public Page<Product> getProductsSortedByName(int page, int size) {
    Pageable pageable = PageRequest.of(page, size, Sort.by("name").ascending());
    return productRepository.findAll(pageable);
}
```

**Controller:**
```java
@GetMapping("/sorted-by-name")
public Page<Product> getProductsSortedByName(@RequestParam(defaultValue = "0") int page,
                                             @RequestParam(defaultValue = "10") int size) {
    return productService.getProductsSortedByName(page, size);
}
```

### Example 2: Sorting by Price Descending
```java
Pageable pageable = PageRequest.of(page, size, Sort.by("price").descending());
```

### Example 3-10
- Sort by `category` ascending.
- Sort by `id` descending.
- Additional field combinations (explored later).

---

## Combining Pagination and Sorting

### Example 1: Paginated and Sorted by Name
```java
public Page<Product> getProductsPaginatedAndSorted(int page, int size, String sortField, String sortDir) {
    Sort sort = Sort.by(sortField).ascending();
    if ("desc".equalsIgnoreCase(sortDir)) {
        sort = Sort.by(sortField).descending();
    }
    Pageable pageable = PageRequest.of(page, size, sort);
    return productRepository.findAll(pageable);
}
```

**Controller:**
```java
@GetMapping("/paged-sorted")
public Page<Product> getPagedSorted(@RequestParam(defaultValue = "0") int page,
                                    @RequestParam(defaultValue = "10") int size,
                                    @RequestParam(defaultValue = "name") String sortField,
                                    @RequestParam(defaultValue = "asc") String sortDir) {
    return productService.getProductsPaginatedAndSorted(page, size, sortField, sortDir);
}
```

**Explanation**: `/products/paged-sorted?page=0&size=10&sortField=name&sortDir=asc` retrieves the first page sorted by name.

### Example 2-10
- Sort by `price` descending.
- Combine with different page sizes and fields.

---

## Advanced Pagination Techniques

### Example 1: Custom Pagination with Offset
```java
public List<Product> getProductsWithOffset(int offset, int limit) {
    return productRepository.findAll(PageRequest.of(offset / limit, limit)).getContent();
}
```

### Example 2: Using `PageRequest` with Sort
Covered in previous sections, extended with complex sorts.

---

## Advanced Sorting Techniques

### Example 1: Dynamic Sorting
See the combined example above—accepts `sortField` and `sortDir` dynamically.

### Example 2: Multi-field Sorting
```java
Pageable pageable = PageRequest.of(page, size, Sort.by("category").ascending().and(Sort.by("price").descending()));
```

---

## Error Handling and Edge Cases

### Example 1: Invalid Page Numbers
```java
if (page < 0 || size <= 0) {
    throw new IllegalArgumentException("Invalid page or size");
}
```

### Example 2: Non-existent Sort Field
Validate `sortField` against entity fields using reflection or a predefined list.

---

## Performance Considerations

### Example 1: Indexing
Add `@Index` to `Product` fields like `name` and `price` in the entity.

### Example 2: Caching
Use Spring’s `@Cacheable` on service methods.

---

## Real-time Examples in E-commerce Domain

### Example 1: Paginating Products by Category
```java
Page<Product> findByCategory(String category, Pageable pageable);
```

### Example 2: Sorting by Popularity
Add a `salesCount` field and sort accordingly.

---

## Testing Pagination and Sorting

### Example 1: Unit Test
```java
@Test
public void testPagination() {
    Page<Product> page = productService.getProducts(0, 10);
    assertEquals(10, page.getSize());
}
```

### Example 2: Integration Test with MockMvc
Test REST endpoints for correct pagination and sorting.

---

## Best Practices and Tips

- **Tip 1**: Choose a default page size (e.g., 10 or 20).
- **Tip 2**: Offer users multiple sorting options (price, name, etc.).
- **Tip 3**: Cache frequently accessed pages.

---
