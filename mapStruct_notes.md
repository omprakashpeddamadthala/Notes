# MapStruct Tutorial: From Basic to Advanced

## Table of Contents

1. [What is MapStruct?](#what-is-mapstruct)
2. [Why Use MapStruct?](#why-use-mapstruct)
3. [Setting Up a Spring Boot Project with MapStruct](#setting-up-a-spring-boot-project-with-mapstruct)
4. [Basic Mapping](#basic-mapping)
   - [Example 1: Simple POJO Mapping](#example-1-simple-pojo-mapping)
   - [Example 2: Mapping with Different Property Names](#example-2-mapping-with-different-property-names)
   - [Example 3: Ignoring Properties](#example-3-ignoring-properties)
   - [Example 4: Mapping with Constants](#example-4-mapping-with-constants)
   - [Example 5: Mapping with Default Values](#example-5-mapping-with-default-values)
   - [Example 6: Mapping Enums](#example-6-mapping-enums)
   - [Example 7: Mapping Dates](#example-7-mapping-dates)
   - [Example 8: Mapping with Inheritance](#example-8-mapping-with-inheritance)
   - [Example 9: Mapping Lists](#example-9-mapping-lists)
   - [Example 10: Bidirectional Mapping](#example-10-bidirectional-mapping)
5. [Intermediate Mapping](#intermediate-mapping)
   - [Custom Mappings](#custom-mappings)
     - [Example 1: Mapping Different Types](#example-1-mapping-different-types)
     - [Example 2: Using Expressions](#example-2-using-expressions)
     - [Example 3: Mapping with Multiple Sources](#example-3-mapping-with-multiple-sources)
     - [Example 4: Inverse Mapping](#example-4-inverse-mapping)
     - [Example 5: Before and After Mapping](#example-5-before-and-after-mapping)
     - [Example 6: Mapping with Default Methods](#example-6-mapping-with-default-methods)
     - [Example 7: Value Mappings for Enums](#example-7-value-mappings-for-enums)
     - [Example 8: Number Formatting](#example-8-number-formatting)
     - [Example 9: Conditional Logic](#example-9-conditional-logic)
     - [Example 10: String Manipulation](#example-10-string-manipulation)
   - [Nested Objects](#nested-objects)
     - [Example 1: Simple Nested Object](#example-1-simple-nested-object)
     - [Example 2: Nested Object with Different Property Names](#example-2-nested-object-with-different-property-names)
     - [Example 3: Flattening Nested Objects](#example-3-flattening-nested-objects)
     - [Example 4: Mapping Collections of Nested Objects](#example-4-mapping-collections-of-nested-objects)
     - [Example 5: Nested Objects with Inheritance](#example-5-nested-objects-with-inheritance)
     - [Example 6: Nested Objects with Custom Mappings](#example-6-nested-objects-with-custom-mappings)
     - [Example 7: Multiple Levels of Nesting](#example-7-multiple-levels-of-nesting)
     - [Example 8: Optional Nested Objects](#example-8-optional-nested-objects)
     - [Example 9: Ignoring Nested Properties](#example-9-ignoring-nested-properties)
     - [Example 10: Nested Objects with Default Values](#example-10-nested-objects-with-default-values)
6. [Advanced Mapping](#advanced-mapping)
   - [Collections](#collections)
     - [Example 1: Mapping List to List](#example-1-mapping-list-to-list)
     - [Example 2: Mapping Set to Set](#example-2-mapping-set-to-set)
     - [Example 3: Mapping Map to Map](#example-3-mapping-map-to-map)
     - [Example 4: Mapping Arrays](#example-4-mapping-arrays)
     - [Example 5: Mapping with Custom Collection Types](#example-5-mapping-with-custom-collection-types)
     - [Example 6: Nested Collections](#example-6-nested-collections)
     - [Example 7: Collection Elements with Different Types](#example-7-collection-elements-with-different-types)
     - [Example 8: Mapping with Filtering](#example-8-mapping-with-filtering)
     - [Example 9: Mapping with Sorting](#example-9-mapping-with-sorting)
     - [Example 10: Mapping with Aggregation](#example-10-mapping-with-aggregation)
   - [Expressions](#expressions)
     - [Example 1: Simple Expression](#example-1-simple-expression)
     - [Example 2: Conditional Expression](#example-2-conditional-expression)
     - [Example 3: Calling Methods](#example-3-calling-methods)
     - [Example 4: Using Constants](#example-4-using-constants)
     - [Example 5: Handling Null Values](#example-5-handling-null-values)
     - [Example 6: Formatting Dates](#example-6-formatting-dates)
     - [Example 7: Calculations](#example-7-calculations)
     - [Example 8: Accessing Nested Properties](#example-8-accessing-nested-properties)
     - [Example 9: Using Utility Classes](#example-9-using-utility-classes)
     - [Example 10: Complex Logic](#example-10-complex-logic)
   - [Dependency Injection](#dependency-injection)
     - [Example 1: Using @Mapper with componentModel](#example-1-using-mapper-with-componentmodel)
     - [Example 2: Injecting Other Mappers](#example-2-injecting-other-mappers)
     - [Example 3: Using @Autowired in Custom Methods](#example-3-using-autowired-in-custom-methods)
     - [Example 4: Constructor Injection](#example-4-constructor-injection)
     - [Example 5: Mapping with Transactional Services](#example-5-mapping-with-transactional-services)
     - [Example 6: Using Qualifiers with Spring Beans](#example-6-using-qualifiers-with-spring-beans)
     - [Example 7: Using MapStruct with Spring Data](#example-7-using-mapstruct-with-spring-data)
     - [Example 8: Configuring MapStruct with Properties](#example-8-configuring-mapstruct-with-properties)
     - [Example 9: Testing Mappers with Spring](#example-9-testing-mappers-with-spring)
     - [Example 10: Layered Architecture](#example-10-layered-architecture)
7. [Complete Code Example](#complete-code-example)
8. [Running and Testing the Project](#running-and-testing-the-project)

---

## What is MapStruct?

MapStruct is an **annotation-based code generator** that automates the mapping between Java bean types, such as entities and Data Transfer Objects (DTOs). It generates efficient, type-safe mapping code at compile time, eliminating the need for manual boilerplate code. This is particularly useful in applications where data needs to be transformed between layers, such as from database entities to API response objects.

---

## Why Use MapStruct?

Here are the key benefits of using MapStruct:

- **Performance**: Generates mapping code at compile time, making it as fast as hand-written code.
- **Type Safety**: Ensures type mismatches are caught during compilation.
- **Less Boilerplate**: Reduces repetitive mapping code, improving maintainability.
- **Ease of Use**: Simple annotations make mappings intuitive to define.
- **Integration**: Seamlessly integrates with frameworks like Spring Boot and tools like Lombok.

---

## Setting Up a Spring Boot Project with MapStruct

To use MapStruct with Spring Boot and Lombok, follow these steps:

1. **Create a Spring Boot Project**: Use Spring Initializr (via [start.spring.io](https://start.spring.io)) or your IDE to create a new project.
2. **Add Dependencies**: Include Spring Boot, MapStruct, and Lombok in your build file.

### Maven (`pom.xml`)

```xml
<dependencies>
    <!-- Spring Boot Starter -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>
    <!-- MapStruct -->
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct</artifactId>
        <version>1.5.2.Final</version>
    </dependency>
    <!-- Lombok -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.24</version>
        <scope>provided</scope>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <annotationProcessorPaths>
                    <path>
                        <groupId>org.mapstruct</groupId>
                        <artifactId>mapstruct-processor</artifactId>
                        <version>1.5.2.Final</version>
                    </path>
                    <path>
                        <groupId>org.projectlombok</groupId>
                        <artifactId>lombok</artifactId>
                        <version>1.18.24</version>
                    </path>
                </annotationProcessorPaths>
            </configuration>
        </plugin>
    </plugins>
</build>
```

### Gradle (`build.gradle`)

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter'
    implementation 'org.mapstruct:mapstruct:1.5.2.Final'
    compileOnly 'org.projectlombok:lombok:1.18.24'
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.5.2.Final'
    annotationProcessor 'org.projectlombok:lombok:1.18.24'
}
```

3. **Configure Lombok**: In your IDE (e.g., IntelliJ IDEA), enable annotation processing and install the Lombok plugin if necessary.

With this setup, you're ready to start mapping!

---

## Basic Mapping

Basic mapping involves straightforward mappings where properties between source and target objects align closely. Here are 10 examples:

### Example 1: Simple POJO Mapping

Mapping a `User` entity to a `UserDto` with identical properties.

```java
// User.java
import lombok.Data;

@Data
public class User {
    private Long id;
    private String name;
    private String email;
}

// UserDto.java
import lombok.Data;

@Data
public class UserDto {
    private Long id;
    private String name;
    private String email;
}

// UserMapper.java
import org.mapstruct.Mapper;
import org.mapstruct.factory.Mappers;

@Mapper
public interface UserMapper {
    UserMapper INSTANCE = Mappers.getMapper(UserMapper.class);

    UserDto userToUserDto(User user);
}
```

**Explanation**: MapStruct automatically maps fields with the same name and type.

---

### Example 2: Mapping with Different Property Names

Mapping `name` to `fullName`.

```java
// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String fullName; // Different name
    private String email;
}

// UserMapper.java
import org.mapstruct.Mapper;
import org.mapstruct.Mapping;

@Mapper
public interface UserMapper {
    @Mapping(source = "name", target = "fullName")
    UserDto userToUserDto(User user);
}
```

**Explanation**: The `@Mapping` annotation specifies the source and target property names.

---

### Example 3: Ignoring Properties

Ignoring the `email` field in the target.

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "email", ignore = true)
    UserDto userToUserDto(User user);
}
```

**Explanation**: `ignore = true` prevents mapping of the specified target property.

---

### Example 4: Mapping with Constants

Setting a constant value for `status`.

```java
// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String name;
    private String email;
    private String status;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "status", constant = "ACTIVE")
    UserDto userToUserDto(User user);
}
```

**Explanation**: The `constant` attribute assigns a fixed value to the target field.

---

### Example 5: Mapping with Default Values

Providing a default `name` if the source is null.

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "name", defaultValue = "Unknown")
    UserDto userToUserDto(User user);
}
```

**Explanation**: `defaultValue` is used when the source property is null.

---

### Example 6: Mapping Enums

Mapping between identical enums.

```java
// Role.java
public enum Role {
    ADMIN, USER
}

// User.java
@Data
public class User {
    private Long id;
    private String name;
    private Role role;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String name;
    private Role role;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: MapStruct maps enums with the same names automatically.

---

### Example 7: Mapping Dates

Mapping `Date` fields directly.

```java
// User.java
import lombok.Data;
import java.util.Date;

@Data
public class User {
    private Long id;
    private String name;
    private Date createdAt;
}

// UserDto.java
import lombok.Data;
import java.util.Date;

@Data
public class UserDto {
    private Long id;
    private String name;
    private Date createdAt;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: Identical types are mapped without additional configuration.

---

### Example 8: Mapping with Inheritance

Mapping inherited classes (simplified example).

```java
// Person.java
@Data
public class Person {
    private String name;
}

// User.java
@Data
public class User extends Person {
    private Long id;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String name;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: MapStruct handles inheritance by mapping properties from both parent and child classes.

---

### Example 9: Mapping Lists

Mapping a list of users.

```java
@Mapper
public interface UserMapper {
    List<UserDto> usersToUserDtos(List<User> users);
}
```

**Explanation**: MapStruct applies the mapping to each element in the collection.

---

### Example 10: Bidirectional Mapping

Mapping from DTO back to entity.

```java
@Mapper
public interface UserMapper {
    UserDto userToUserDto(User user);

    User userDtoToUser(UserDto userDto);
}
```

**Explanation**: Define both directions explicitly for bidirectional mapping.

---

## Intermediate Mapping

Intermediate mappings involve more complex scenarios like custom transformations and nested objects.

### Custom Mappings

Custom mappings handle cases where automatic mapping isn’t sufficient.

#### Example 1: Mapping Different Types

Converting `Date` to `String`.

```java
// User.java
@Data
public class User {
    private Long id;
    private String name;
    private Date birthDate;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String name;
    private String birthDate;
}

// UserMapper.java
import org.mapstruct.Mapper;
import org.mapstruct.Named;
import java.util.Date;

@Mapper
public interface UserMapper {
    @Mapping(source = "birthDate", target = "birthDate", qualifiedByName = "dateToString")
    UserDto userToUserDto(User user);

    @Named("dateToString")
    default String dateToString(Date date) {
        return date != null ? date.toString() : null;
    }
}
```

**Explanation**: A custom method with `@Named` handles the type conversion.

---

#### Example 2: Using Expressions

Combining `firstName` and `lastName`.

```java
// User.java
@Data
public class User {
    private Long id;
    private String firstName;
    private String lastName;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String fullName;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "fullName", expression = "java(user.getFirstName() + \" \" + user.getLastName())")
    UserDto userToUserDto(User user);
}
```

**Explanation**: `expression` allows inline Java code for mapping.

---

#### Example 3: Mapping with Multiple Sources

Combining `User` and `Address` into `UserDto`.

```java
// Address.java
@Data
public class Address {
    private String city;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(source = "user.id", target = "id")
    @Mapping(source = "address.city", target = "city")
    UserDto userAndAddressToUserDto(User user, Address address);
}
```

**Explanation**: Multiple source objects are mapped into one target.

---

#### Example 4: Inverse Mapping

Bidirectional mapping with inverse configuration.

```java
@Mapper
public interface UserMapper {
    @Mapping(source = "name", target = "fullName")
    UserDto userToUserDto(User user);

    @InheritInverseConfiguration
    User userDtoToUser(UserDto userDto);
}
```

**Explanation**: `@InheritInverseConfiguration` reuses the inverse mapping rules.

---

#### Example 5: Before and After Mapping

Adding logic before and after mapping.

```java
@Mapper
public interface UserMapper {
    @BeforeMapping
    default void beforeMapping(User user) {
        System.out.println("Mapping user: " + user.getName());
    }

    UserDto userToUserDto(User user);

    @AfterMapping
    default void afterMapping(User user, @MappingTarget UserDto userDto) {
        userDto.setName(userDto.getName().toUpperCase());
    }
}
```

**Explanation**: `@BeforeMapping` and `@AfterMapping` hooks allow custom logic.

---

#### Example 6: Mapping with Default Methods

Manual mapping with a default method.

```java
@Mapper
public interface UserMapper {
    default UserDto userToUserDto(User user) {
        if (user == null) return null;
        UserDto dto = new UserDto();
        dto.setId(user.getId());
        dto.setName("Prefix-" + user.getName());
        return dto;
    }
}
```

**Explanation**: Default methods allow full control over mapping logic.

---

#### Example 7: Value Mappings for Enums

Mapping enums to strings.

```java
@Mapper
public interface UserMapper {
    @ValueMappings({
        @ValueMapping(source = "ADMIN", target = "Administrator"),
        @ValueMapping(source = "USER", target = "Regular User")
    })
    String mapRole(Role role);

    UserDto userToUserDto(User user);
}
```

**Explanation**: `@ValueMappings` defines specific enum-to-string mappings.

---

#### Example 8: Number Formatting

Formatting a `double` to a `String`.

```java
// User.java
@Data
public class User {
    private Long id;
    private double salary;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String salary;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "salary", expression = "java(String.format(\"%.2f\", user.getSalary()))")
    UserDto userToUserDto(User user);
}
```

**Explanation**: An expression formats the number.

---

#### Example 9: Conditional Logic

Conditional mapping of `status`.

```java
// User.java
@Data
public class User {
    private Long id;
    private boolean active;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String status;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "status", expression = "java(user.isActive() ? \"Active\" : \"Inactive\")")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Expressions support conditional logic.

---

#### Example 10: String Manipulation

Uppercasing a string.

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "name", qualifiedByName = "toUpperCase")
    UserDto userToUserDto(User user);

    @Named("toUpperCase")
    default String toUpperCase(String name) {
        return name != null ? name.toUpperCase() : null;
    }
}
```

**Explanation**: A custom method transforms the string.

---

### Nested Objects

Nested object mappings involve mapping properties within embedded objects.

#### Example 1: Simple Nested Object

Mapping `User` with an `Address`.

```java
// Address.java
@Data
public class Address {
    private String street;
    private String city;
}

// User.java
@Data
public class User {
    private Long id;
    private String name;
    private Address address;
}

// AddressDto.java
@Data
public class AddressDto {
    private String street;
    private String city;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String name;
    private AddressDto address;
}

// AddressMapper.java
@Mapper
public interface AddressMapper {
    AddressDto addressToAddressDto(Address address);
}

// UserMapper.java
@Mapper(uses = AddressMapper.class)
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: `uses` links the nested mapper.

---

#### Example 2: Nested Object with Different Property Names

Mapping `street` to `road`.

```java
// AddressDto.java
@Data
public class AddressDto {
    private String road; // Different name
    private String city;
}

// AddressMapper.java
@Mapper
public interface AddressMapper {
    @Mapping(source = "street", target = "road")
    AddressDto addressToAddressDto(Address address);
}
```

**Explanation**: `@Mapping` adjusts property names in nested objects.

---

#### Example 3: Flattening Nested Objects

Mapping `address.city` to `city`.

```java
// UserDto.java
@Data
public class UserDto {
    private Long id;
    private String name;
    private String city;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(source = "address.city", target = "city")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Dot notation flattens nested properties.

---

#### Example 4: Mapping Collections of Nested Objects

Mapping a list of addresses.

```java
// User.java
@Data
public class User {
    private Long id;
    private List<Address> addresses;
}

// UserDto.java
@Data
public class UserDto {
    private Long id;
    private List<AddressDto> addresses;
}

// UserMapper.java
@Mapper(uses = AddressMapper.class)
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: Collections are mapped element-by-element using the nested mapper.

---

#### Example 5: Nested Objects with Inheritance

Mapping inherited nested objects (simplified).

```java
// Address.java
@Data
public class Address {
    private String street;
}

// HomeAddress.java
@Data
public class HomeAddress extends Address {
    private String city;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: MapStruct maps inherited properties if types align.

---

#### Example 6: Nested Objects with Custom Mappings

Custom mapping within a nested object.

```java
// AddressMapper.java
@Mapper
public interface AddressMapper {
    @Mapping(source = "street", target = "street", qualifiedByName = "formatStreet")
    AddressDto addressToAddressDto(Address address);

    @Named("formatStreet")
    default String formatStreet(String street) {
        return street.toUpperCase();
    }
}
```

**Explanation**: Custom methods apply to nested properties.

---

#### Example 7: Multiple Levels of Nesting

Mapping `User -> Address -> Country`.

```java
// Country.java
@Data
public class Country {
    private String name;
}

// Address.java
@Data
public class Address {
    private String street;
    private Country country;
}

// User.java
@Data
public class User {
    private Address address;
}

// CountryDto.java
@Data
public class CountryDto {
    private String name;
}

// AddressDto.java
@Data
public class AddressDto {
    private String street;
    private CountryDto country;
}

// CountryMapper.java
@Mapper
public interface CountryMapper {
    CountryDto countryToCountryDto(Country country);
}

// AddressMapper.java
@Mapper(uses = CountryMapper.class)
public interface AddressMapper {
    AddressDto addressToAddressDto(Address address);
}

// UserMapper.java
@Mapper(uses = AddressMapper.class)
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: Multiple mappers handle each nesting level.

---

#### Example 8: Optional Nested Objects

Handling null nested objects.

```java
@Mapper(uses = AddressMapper.class)
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: MapStruct sets the target to null if the source nested object is null.

---

#### Example 9: Ignoring Nested Properties

Ignoring `city` in `AddressDto`.

```java
// AddressMapper.java
@Mapper
public interface AddressMapper {
    @Mapping(target = "city", ignore = true)
    AddressDto addressToAddressDto(Address address);
}
```

**Explanation**: `ignore` applies to nested properties.

---

#### Example 10: Nested Objects with Default Values

Setting a default for `city`.

```java
// AddressMapper.java
@Mapper
public interface AddressMapper {
    @Mapping(target = "city", defaultValue = "Unknown")
    AddressDto addressToAddressDto(Address address);
}
```

**Explanation**: Default values work for nested properties.

---

## Advanced Mapping

Advanced mappings cover collections, expressions, and dependency injection.

### Collections

Mapping various collection types and scenarios.

#### Example 1: Mapping List to List

```java
@Mapper
public interface UserMapper {
    List<UserDto> usersToUserDtos(List<User> users);
}
```

**Explanation**: Standard list mapping.

---

#### Example 2: Mapping Set to Set

```java
@Mapper
public interface UserMapper {
    Set<UserDto> usersToUserDtos(Set<User> users);
}
```

**Explanation**: Works similarly for sets.

---

#### Example 3: Mapping Map to Map

```java
@Mapper
public interface UserMapper {
    Map<String, UserDto> mapUsers(Map<Long, User> userMap);
}
```

**Explanation**: Maps keys and values as specified.

---

#### Example 4: Mapping Arrays

```java
@Mapper
public interface UserMapper {
    UserDto[] usersToUserDtos(User[] users);
}
```

**Explanation**: Arrays are mapped element-by-element.

---

#### Example 5: Mapping with Custom Collection Types

Using a custom list (simplified).

```java
@Mapper
public interface UserMapper {
    List<UserDto> usersToUserDtos(List<User> users); // Custom list handled by standard mapping
}
```

**Explanation**: Standard collections don’t need special handling.

---

#### Example 6: Nested Collections

Mapping `List<List<User>>`.

```java
@Mapper
public interface UserMapper {
    List<List<UserDto>> nestedUsersToDtos(List<List<User>> users);
}
```

**Explanation**: Nested collections are recursively mapped.

---

#### Example 7: Collection Elements with Different Types

Mapping `List<String>` to `List<Integer>`.

```java
@Mapper
public interface UserMapper {
    @Mapping(target = ".", qualifiedByName = "stringToInteger")
    List<Integer> stringsToIntegers(List<String> strings);

    @Named("stringToInteger")
    default Integer stringToInteger(String s) {
        return Integer.parseInt(s);
    }
}
```

**Explanation**: Custom methods transform collection elements.

---

#### Example 8: Mapping with Filtering

Filtering before mapping (manual).

```java
@Mapper
public interface UserMapper {
    default List<UserDto> activeUsersToDtos(List<User> users) {
        return users.stream()
            .filter(User::isActive)
            .map(this::userToUserDto)
            .collect(Collectors.toList());
    }

    UserDto userToUserDto(User user);
}
```

**Explanation**: Filtering requires custom logic.

---

#### Example 9: Mapping with Sorting

Sorting after mapping.

```java
@Mapper
public interface UserMapper {
    default List<UserDto> sortedUsersToDtos(List<User> users) {
        List<UserDto> dtos = usersToUserDtos(users);
        dtos.sort(Comparator.comparing(UserDto::getName));
        return dtos;
    }

    List<UserDto> usersToUserDtos(List<User> users);
}
```

**Explanation**: Sorting is handled manually.

---

#### Example 10: Mapping with Aggregation

Calculating a total from a list.

```java
// Order.java
@Data
public class Order {
    private double amount;
}

// User.java
@Data
public class User {
    private List<Order> orders;
}

// UserDto.java
@Data
public class UserDto {
    private double totalAmount;
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "totalAmount", qualifiedByName = "calculateTotal")
    UserDto userToUserDto(User user);

    @Named("calculateTotal")
    default double calculateTotal(List<Order> orders) {
        return orders.stream().mapToDouble(Order::getAmount).sum();
    }
}
```

**Explanation**: Aggregation uses a custom method.

---

### Expressions

Expressions embed Java code in mappings.

#### Example 1: Simple Expression

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "fullName", expression = "java(user.getFirstName() + \" \" + user.getLastName())")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Concatenates strings directly.

---

#### Example 2: Conditional Expression

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "status", expression = "java(user.isActive() ? \"Active\" : \"Inactive\")")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Uses ternary operator for conditions.

---

#### Example 3: Calling Methods

```java
// User.java
@Data
public class User {
    private int age;
    public int calculateAge() { return age; }
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "age", expression = "java(user.calculateAge())")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Calls a method on the source object.

---

#### Example 4: Using Constants

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "type", expression = "java(\"User\")")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Sets a constant value via expression.

---

#### Example 5: Handling Null Values

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "name", expression = "java(user.getName() != null ? user.getName() : \"Unknown\")")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Handles null checks inline.

---

#### Example 6: Formatting Dates

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "birthDate", expression = "java(new java.text.SimpleDateFormat(\"yyyy-MM-dd\").format(user.getBirthDate()))")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Formats a date using an expression.

---

#### Example 7: Calculations

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "discount", expression = "java(user.getTotalSpent() > 1000 ? 0.1 : 0.0)")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Performs a calculation.

---

#### Example 8: Accessing Nested Properties

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "city", expression = "java(user.getAddress().getCity())")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Accesses nested properties (though dot notation is preferred).

---

#### Example 9: Using Utility Classes

```java
// Utils.java
public class Utils {
    public static String encode(String value) {
        return value.toUpperCase();
    }
}

// UserMapper.java
@Mapper
public interface UserMapper {
    @Mapping(target = "encodedName", expression = "java(com.example.Utils.encode(user.getName()))")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Calls a static utility method.

---

#### Example 10: Complex Logic

```java
@Mapper
public interface UserMapper {
    @Mapping(target = "description", expression = "java(user.getName() + (user.isActive() ? \" is active\" : \" is inactive\"))")
    UserDto userToUserDto(User user);
}
```

**Explanation**: Combines multiple operations (better moved to a custom method for readability).

---

### Dependency Injection

Integrating MapStruct with Spring’s dependency injection.

#### Example 1: Using @Mapper with componentModel

```java
@Mapper(componentModel = "spring")
public interface UserMapper {
    UserDto userToUserDto(User user);
}

// UserService.java
@Service
public class UserService {
    @Autowired
    private UserMapper userMapper;
}
```

**Explanation**: `componentModel = "spring"` makes the mapper a Spring bean.

---

#### Example 2: Injecting Other Mappers

```java
@Mapper(componentModel = "spring", uses = AddressMapper.class)
public interface UserMapper {
    UserDto userToUserDto(User user);
}
```

**Explanation**: Spring injects the `AddressMapper` bean.

---

#### Example 3: Using @Autowired in Custom Methods

```java
@Mapper(componentModel = "spring")
public abstract class UserMapper {
    @Autowired
    private SomeService someService;

    @Mapping(target = "someField", expression = "java(someService.calculateSomething(user))")
    public abstract UserDto userToUserDto(User user);
}
```

**Explanation**: Abstract class allows field injection.

---

#### Example 4: Constructor Injection

```java
@Mapper(componentModel = "spring")
public abstract class UserMapper {
    private final SomeService someService;

    @Autowired
    public UserMapper(SomeService someService) {
        this.someService = someService;
    }

    @Mapping(target = "someField", expression = "java(someService.calculateSomething(user))")
    public abstract UserDto userToUserDto(User user);
}
```

**Explanation**: Constructor injection is preferred in Spring.

---

#### Example 5: Mapping with Transactional Services

```java
@Service
public class UserService {
    @Autowired
    private UserMapper userMapper;

    @Transactional
    public UserDto getUser(Long id) {
        User user = // fetch from DB
        return userMapper.userToUserDto(user);
    }
}
```

**Explanation**: Mapping occurs within a transaction, though it’s typically pure.

---

#### Example 6: Using Qualifiers with Spring Beans

```java
@Service
@Qualifier("nameFormatter")
public class NameFormatter {
    public String format(String name) { return name.toUpperCase(); }
}

@Mapper(componentModel = "spring", uses = NameFormatter.class)
public interface UserMapper {
    @Mapping(target = "name", qualifiedByName = "format")
    UserDto userToUserDto(User user);
}
```

**Explanation**: `@Qualifier` disambiguates beans.

---

#### Example 7: Using MapStruct with Spring Data

```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
    @Autowired
    private UserMapper userMapper;

    public UserDto getUser(Long id) {
        User user = userRepository.findById(id).orElseThrow();
        return userMapper.userToUserDto(user);
    }
}
```

**Explanation**: Maps entities from Spring Data to DTOs.

---

#### Example 8: Configuring MapStruct with Properties

```properties
# application.properties
mapstruct.defaultComponentModel=spring
mapstruct.unmappedTargetPolicy=ERROR
```

**Explanation**: Configures MapStruct via Spring Boot properties.

---

#### Example 9: Testing Mappers with Spring

```java
@SpringBootTest
public class UserMapperTest {
    @Autowired
    private UserMapper userMapper;

    @Test
    public void testMapping() {
        User user = new User();
        user.setName("John");
        UserDto dto = userMapper.userToUserDto(user);
        assertEquals("John", dto.getName());
    }
}
```

**Explanation**: Uses Spring context for testing.

---

#### Example 10: Layered Architecture

```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
    @Autowired
    private UserMapper userMapper;

    public UserDto getUser(Long id) {
        User user = userRepository.findById(id).orElseThrow();
        return userMapper.userToUserDto(user);
    }
}
```

**Explanation**: Typical use in a service layer.

---

## Complete Code Example

Here’s a full example integrating the concepts above.

### Entities

```java
// User.java
import lombok.Data;
import javax.persistence.*;
import java.util.List;

@Entity
@Data
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String firstName;
    private String lastName;
    private String email;
    @OneToMany(cascade = CascadeType.ALL)
    private List<Address> addresses;
}

// Address.java
import lombok.Data;
import javax.persistence.*;

@Entity
@Data
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String street;
    private String city;
}
```

### DTOs

```java
// UserDto.java
import lombok.Data;
import java.util.List;

@Data
public class UserDto {
    private Long id;
    private String fullName;
    private String email;
    private List<AddressDto> addresses;
    private String primaryCity;
}

// AddressDto.java
import lombok.Data;

@Data
public class AddressDto {
    private String street;
    private String city;
}
```

### Mappers

```java
// AddressMapper.java
@Mapper(componentModel = "spring")
public interface AddressMapper {
    AddressDto addressToAddressDto(Address address);
}

// UserMapper.java
@Mapper(componentModel = "spring", uses = AddressMapper.class)
public interface UserMapper {
    @Mapping(source = "firstName", target = "fullName", expression = "java(user.getFirstName() + \" \" + user.getLastName())")
    @Mapping(source = "addresses", target = "primaryCity", qualifiedByName = "getPrimaryCity")
    UserDto userToUserDto(User user);

    @Named("getPrimaryCity")
    default String getPrimaryCity(List<Address> addresses) {
        return addresses.stream().findFirst().map(Address::getCity).orElse("Unknown");
    }
}
```

### Service and Controller

```java
// UserRepository.java
public interface UserRepository extends JpaRepository<User, Long> {}

// UserService.java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
    @Autowired
    private UserMapper userMapper;

    public UserDto getUser(Long id) {
        User user = userRepository.findById(id).orElseThrow();
        return userMapper.userToUserDto(user);
    }
}

// UserController.java
@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public UserDto getUser(@PathVariable Long id) {
        return userService.getUser(id);
    }
}
```

### Dependencies

Add Spring Data JPA to `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

---

## Running and Testing the Project

1. **Configure Database**:
   ```properties
   # application.properties
   spring.datasource.url=jdbc:h2:mem:testdb
   spring.datasource.driverClassName=org.h2.Driver
   spring.datasource.username=sa
   spring.datasource.password=
   spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
   spring.h2.console.enabled=true
   ```

2. **Run the Application**:
   - Use your IDE or run `mvn spring-boot:run`.

3. **Test the API**:
   - Use Postman or curl: `GET http://localhost:8080/users/1`
   - Pre-populate the database with a `User` entity for testing.

This completes the tutorial, covering MapStruct from basic to advanced usage with Spring Boot and Lombok! For the full project, consider creating a GitHub repository with the code.
