
---

# Spring Boot Data Mappings and Relationships Tutorial

## Table of Contents

1. [Introduction](#introduction)
2. [Setting Up the Project](#setting-up-the-project)
3. [Basic Entity Mapping](#basic-entity-mapping)
   - [Example 1: Product Entity](#example-1-product-entity)
   - [Example 2: Category Entity](#example-2-category-entity)
4. [One-to-One Relationship](#one-to-one-relationship)
   - [Example 1: Unidirectional One-to-One](#example-1-unidirectional-one-to-one)
   - [Example 2: Bidirectional One-to-One](#example-2-bidirectional-one-to-one)
   - [Example 3: One-to-One with Shared Primary Key](#example-3-one-to-one-with-shared-primary-key)
5. [One-to-Many and Many-to-One Relationships](#one-to-many-and-many-to-one-relationships)
   - [Example 1: Unidirectional One-to-Many](#example-1-unidirectional-one-to-many)
   - [Example 2: Bidirectional One-to-Many](#example-2-bidirectional-one-to-many)
   - [Example 3: Cascade Operations](#example-3-cascade-operations)
   - [Example 4: Fetch Types](#example-4-fetch-types)
6. [Many-to-Many Relationship](#many-to-many-relationship)
   - [Example 1: Basic Many-to-Many](#example-1-basic-many-to-many)
   - [Example 2: Many-to-Many with Intermediate Entity](#example-2-many-to-many-with-intermediate-entity)
   - [Example 3: Bidirectional Many-to-Many](#example-3-bidirectional-many-to-many)
7. [Advanced Topics](#advanced-topics)
   - [Cascade Types](#cascade-types)
   - [Fetch Types](#fetch-types)
   - [Embedded Types](#embedded-types)
   - [Composite Keys](#composite-keys)

---

## Introduction

Spring Boot simplifies Java application development, and **Spring Data JPA** makes database interactions effortless by providing a layer over Hibernate. In this tutorial, we’ll explore **entity mappings and relationships**, which define how data entities (e.g., tables in a database) are connected. We’ll use an **e-commerce domain** with entities like `Customer`, `Order`, `Product`, `Category`, and `Address` to illustrate these concepts.

We’ll leverage **Lombok** to reduce boilerplate code (e.g., getters, setters) in our entities. The tutorial progresses from basic mappings to advanced relationship configurations, with detailed code snippets and explanations.

---

## Setting Up the Project

To follow along, set up a Spring Boot project with the following dependencies:

- **Spring Web**
- **Spring Data JPA**
- **H2 Database** (for simplicity)
- **Lombok**

### Steps

1. Use **Spring Initializr** (https://start.spring.io/) to generate a project with these dependencies.
2. Add the dependencies to your `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

3. Configure `application.properties` for the H2 database:

```properties
spring.datasource.url=jdbc:h2:mem:ecommerce
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update
```

4. Ensure Lombok is enabled in your IDE (e.g., install the Lombok plugin in IntelliJ or Eclipse).

This setup provides an in-memory H2 database, accessible via `http://localhost:8080/h2-console`.

---

## Basic Entity Mapping

Let’s start with simple entities to understand basic mappings.

### Example 1: Product Entity

The `Product` entity represents items in our e-commerce store.

```java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import javax.persistence.*;

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    private double price;
}
```

- **@Entity**: Marks this class as a JPA entity, mapped to a database table (`product` by default).
- **@Id**: Specifies the primary key.
- **@GeneratedValue**: Auto-increments the `id`.
- **@Column**: Customizes column properties (e.g., `nullable = false` ensures `name` is required).
- **Lombok Annotations**: `@Data` generates getters, setters, `toString`, etc.; `@NoArgsConstructor` and `@AllArgsConstructor` provide constructors.

**Repository**:

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

**Usage**:

```java
Product product = new Product(null, "Laptop", 999.99);
productRepository.save(product);
```

### Example 2: Category Entity

The `Category` entity groups products.

```java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import javax.persistence.*;

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;
}
```

Similar to `Product`, this is a basic entity with an `id` and `name`.

---

## One-to-One Relationship

A one-to-one relationship means each entity instance is related to exactly one instance of another entity. Let’s use `Customer` and `Address`.

### Example 1: Unidirectional One-to-One

`Customer` has an `Address`, but `Address` doesn’t reference `Customer`.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    @OneToOne
    @JoinColumn(name = "address_id")
    private Address address;
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String street;
    private String city;
}
```

- **@OneToOne**: Defines the relationship.
- **@JoinColumn**: Adds an `address_id` foreign key to the `customer` table.

**Usage**:

```java
Address address = new Address(null, "123 Main St", "Anytown");
addressRepository.save(address);

Customer customer = new Customer(null, "John Doe", "john@example.com", address);
customerRepository.save(customer);
```

### Example 2: Bidirectional One-to-One

Add a reference from `Address` back to `Customer`.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    @OneToOne
    @JoinColumn(name = "address_id")
    private Address address;
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String street;
    private String city;

    @OneToOne(mappedBy = "address")
    private Customer customer;
}
```

- **mappedBy**: Indicates that the `Customer` entity owns the relationship, avoiding duplicate foreign keys.

### Example 3: One-to-One with Shared Primary Key

`Address` uses the same `id` as `Customer`.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToOne(cascade = CascadeType.ALL)
    @PrimaryKeyJoinColumn
    private Address address;
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Address {
    @Id
    private Long id;
    private String street;

    @MapsId
    @OneToOne(mappedBy = "address")
    private Customer customer;
}
```

- **@PrimaryKeyJoinColumn**: Shares the primary key.
- **@MapsId**: Maps `Address`’s `id` to `Customer`’s.

---

## One-to-Many and Many-to-One Relationships

These relationships are two sides of the same coin. Let’s use `Customer` and `Order`.

### Example 1: Unidirectional One-to-Many

`Customer` has many `Order`s.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToMany
    @JoinColumn(name = "customer_id")
    private List<Order> orders = new ArrayList<>();
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Order {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Date orderDate;
}
```

- **@OneToMany**: Indicates a collection of `Order`s.
- **@JoinColumn**: Adds a `customer_id` foreign key to the `order` table.

### Example 2: Bidirectional One-to-Many

Add a reference from `Order` to `Customer`.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToMany(mappedBy = "customer")
    private List<Order> orders = new ArrayList<>();
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Order {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Date orderDate;

    @ManyToOne
    @JoinColumn(name = "customer_id")
    private Customer customer;
}
```

- **@ManyToOne**: Defines the inverse side.

### Example 3: Cascade Operations

Persist `Order`s when saving a `Customer`.

```java
@OneToMany(mappedBy = "customer", cascade = CascadeType.PERSIST)
private List<Order> orders = new ArrayList<>();
```

**Usage**:

```java
Customer customer = new Customer(null, "Jane Doe");
Order order = new Order(null, new Date());
customer.getOrders().add(order);
order.setCustomer(customer);
customerRepository.save(customer);
```

- **cascade**: Propagates operations (e.g., persist, remove) to related entities.

### Example 4: Fetch Types

Control how related data is loaded.

```java
@OneToMany(mappedBy = "customer", fetch = FetchType.LAZY)
private List<Order> orders = new ArrayList<>();
```

- **FetchType.LAZY**: Loads `orders` only when accessed (default for `@OneToMany`).
- **FetchType.EAGER**: Loads `orders` immediately (default for `@ManyToOne`).

---

## Many-to-Many Relationship

A many-to-many relationship involves multiple connections, like `Product` and `Category`.

### Example 1: Basic Many-to-Many

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @ManyToMany
    @JoinTable(
        name = "product_category",
        joinColumns = @JoinColumn(name = "product_id"),
        inverseJoinColumns = @JoinColumn(name = "category_id")
    )
    private List<Category> categories = new ArrayList<>();
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}
```

- **@ManyToMany**: Creates a join table (`product_category`).

### Example 2: Many-to-Many with Intermediate Entity

For extra fields (e.g., `addedDate`), use an intermediate entity.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToMany(mappedBy = "product")
    private List<ProductCategory> productCategories = new ArrayList<>();
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToMany(mappedBy = "category")
    private List<ProductCategory> productCategories = new ArrayList<>();
}

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
@Table(name = "product_category")
public class ProductCategory {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "product_id")
    private Product product;

    @ManyToOne
    @JoinColumn(name = "category_id")
    private Category category;

    private Date addedDate;
}
```

### Example 3: Bidirectional Many-to-Many

Add the inverse mapping.

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @ManyToMany(mappedBy = "categories")
    private List<Product> products = new ArrayList<>();
}
```

---

## Advanced Topics

### Cascade Types

Control how operations propagate (e.g., `CascadeType.ALL`, `CascadeType.REMOVE`).

### Fetch Types

Optimize loading with `LAZY` or `EAGER`.

### Embedded Types

Use `@Embeddable` for reusable components like `Address`.

```java
@Embeddable
@Data
public class Address {
    private String street;
    private String city;
}

@Entity
@Data
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @Embedded
    private Address address;
}
```

### Composite Keys

Use `@EmbeddedId` for complex keys.

```java
@Embeddable
@Data
public class OrderItemKey implements Serializable {
    private Long orderId;
    private Long productId;
}

@Entity
@Data
public class OrderItem {
    @EmbeddedId
    private OrderItemKey id;

    @ManyToOne
    @MapsId("orderId")
    @JoinColumn(name = "order_id")
    private Order order;

    @ManyToOne
    @MapsId("productId")
    @JoinColumn(name = "product_id")
    private Product product;

    private int quantity;
}
```

---
