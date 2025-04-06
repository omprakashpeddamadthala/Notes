# Java Stream Collectors

This document provides an overview of various collectors available in Java Streams, including their descriptions, return types, examples, and real-time use cases where applicable. Below is a navigable table of contents linking to each collector's section, followed by beautifully formatted details for each collector in Markdown syntax.

## Table of Contents

- [partitioningBy](#partitioningby)
- [counting](#counting)
- [summarizingInt](#summarizingint)
- [mapping](#mapping)
- [joining with delimiter, prefix, and suffix](#joining-with-delimiter-prefix-and-suffix)
- [groupingBy with downstream collector](#groupingby-with-downstream-collector)
- [filtering](#filtering)
- [collectingAndThen](#collectingandthen)
- [mapping with downstream collector](#mapping-with-downstream-collector)
- [toMap](#tomap)
- [toConcurrentMap](#toconcurrentmap)
- [reducing](#reducing)
- [flatMapping](#flatmapping)
- [summarizingDouble](#summarizingdouble)
- [summarizingLong](#summarizinglong)
- [groupingByConcurrent](#groupingbyconcurrent)
- [teeing](#teeing)

---

## partitioningBy

The `partitioningBy` method in Java Streams is used to partition the elements of a stream into two groups based on a specified predicate. It returns a `Map` where the keys are `Boolean`, and the values are lists of elements that satisfy (or do not satisfy) the predicate.

**Return Type:** `Map<Boolean, List<T>>` where:
- Key `true` contains elements that satisfy the predicate.
- Key `false` contains elements that do not satisfy the predicate.

**Example:**

**Question:** Partition a list of integers into even and odd numbers.

**Solution:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
Map<Boolean, List<Integer>> result = numbers.stream()
                                           .collect(Collectors.partitioningBy(n -> n % 2 == 0));
System.out.println(result);
```

**Output:**

```
{false=[1, 3, 5], true=[2, 4, 6]}
```

**Real-time Use Case:**

**Predicate:** Customers whose lifetime spending exceeds a certain threshold (e.g., $10,000).

**True group:** High-value customers (VIPs).

**False group:** Regular customers.

```java
Map<Boolean, List<Customer>> customerPartition = customerList.stream()
    .collect(Collectors.partitioningBy(customer -> customer.getTotalSpend() > 10000));
```

---

## counting

The `counting` method in Java Streams is a collector that counts the number of elements in the stream. It’s often used in conjunction with other collectors for aggregation.

**Return Type:** `Collector<T, ?, Long>` that counts the elements in the stream.

**Example:**

**Question:** Count the number of strings in a list.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
long count = words.stream()
                  .collect(Collectors.counting());
System.out.println(count);
```

**Output:**

```
3
```

**Real-time Use Case:**

Counting the total number of orders placed by customers over a given period.

```java
long totalOrders = orderList.stream()
    .collect(Collectors.counting());
```

**Use Case:** Useful for generating daily, weekly, or monthly sales reports to measure business performance.

---

## summarizingInt

The `summarizingInt` method in Java Streams is a collector that generates summary statistics for the elements of a stream, including count, sum, minimum, average, and maximum.

**Return Type:** `IntSummaryStatistics` object containing the summary statistics.

**Example:**

**Question:** Generate summary statistics (count, sum, min, average, max) for a list of integers.

**Solution:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
IntSummaryStatistics stats = numbers.stream()
                                    .collect(Collectors.summarizingInt(Integer::intValue));
System.out.println(stats);
```

**Output:**

```
IntSummaryStatistics{count=5, sum=15, min=1, average=3.000000, max=5}
```

---

## mapping

The `mapping` method in Java Streams is used to apply a mapping function to the elements of a stream and then collect the results using another collector.

**Return Type:** `Collector` that applies a mapping function and collects the results.

**Example:**

**Question:** Extract and collect the lengths of all strings in a list.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
List<Integer> lengths = words.stream()
                             .collect(Collectors.mapping(String::length, Collectors.toList()));
System.out.println(lengths);
```

**Output:**

```
[5, 6, 6]
```

**Real-time Use Case:**

Extract customer email addresses from a list of orders to create a list for sending marketing or order status updates.

```java
List<String> customerEmails = orderList.stream()
    .collect(Collectors.mapping(order -> order.getCustomer().getEmail(), Collectors.toList()));
```

---

## joining with delimiter, prefix, and suffix

The `joining` method in Java Streams concatenates the elements of a stream into a single `String`, with optional delimiters, prefix, and suffix.

**Return Type:** `Collector` that concatenates the elements of a stream into a single `String`.

**Example:**

**Question:** Concatenate all strings in a list into a single string with commas, a prefix, and a suffix.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
String result = words.stream()
                     .collect(Collectors.joining(", ", "[", "]"));
System.out.println(result);
```

**Output:**

```
[apple, banana, cherry]
```

---

## groupingBy with downstream collector

The `groupingBy` method in Java Streams groups the elements of the stream by a classifier function and can also apply a downstream collector to the results.

**Return Type:** `Map<K, D>` where `K` is the type of the classifier, and `D` is the result of the downstream collector.

**Example:**

**Question:** Group a list of strings by their length and count the number of strings in each group.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "date");
Map<Integer, Long> groupedByLength = words.stream()
                                          .collect(Collectors.groupingBy(String::length, Collectors.counting()));
System.out.println(groupedByLength);
```

**Output:**

```
{4=1, 5=1, 6=2}
```

**Real-time Use Case:**

Group orders by customer and count how many orders each customer has placed using `counting` as a downstream collector.

```java
Map<Customer, Long> ordersByCustomer = orderList.stream()
    .collect(Collectors.groupingBy(Order::getCustomer, Collectors.counting()));
```

**Use Case:** Generate reports on the number of orders per customer to understand loyalty, identify frequent buyers, and tailor marketing efforts.

---

## filtering

The `filtering` method filters stream elements and then collects the results using another collector.

**Return Type:** `Collector` that filters elements and collects the results.

**Example:**

**Question:** Filter and collect only the even numbers from a list of integers.

**Solution:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> evens = numbers.stream()
                             .collect(Collectors.filtering(n -> n % 2 == 0, Collectors.toList()));
System.out.println(evens);
```

**Output:**

```
[2, 4, 6, 8, 10]
```

**Real-time Use Case:**

Analyze high-value orders (e.g., above $500) by filtering and collecting them into a list.

```java
List<Order> highValueOrders = orderList.stream()
    .collect(Collectors.filtering(order -> order.getTotalAmount() > 500, Collectors.toList()));
```

**Use Case:** Generate reports of high-value orders for special customer service, fraud detection, or VIP treatment.

**Difference Between `filter` and `filtering`:**

| Aspect              | Filter                                    | Filtering                                                      |
|---------------------|-------------------------------------------|----------------------------------------------------------------|
| **When Applied**    | Before any terminal operation (early)     | As part of a downstream collector (after grouping, etc.)       |
| **Where It Acts**   | Filters the entire stream                 | Filters within a collection step (e.g., inside a group)        |
| **Common Use Case** | Filter stream before processing           | Filter elements within a group or collection context           |
| **Typical Usage**   | `.filter(predicate).collect(...)`         | `.collect(Collectors.groupingBy(..., Collectors.filtering(...)))` |

---

## collectingAndThen

The `collectingAndThen` method in Java Streams first applies a collection operation and then applies another function to the result.

**Return Type:** `Collector<T, A, R>` that first collects elements and then transforms the result.

**Example:**

**Question:** Convert a stream of strings into a set and then get its size.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "banana");
int size = words.stream()
                .collect(Collectors.collectingAndThen(Collectors.toSet(), Set::size));
System.out.println(size);
```

**Output:**

```
3
```

**Real-time Use Case:**

Collect customers into a set and transform it into a list of email addresses.

```java
List<String> customerEmails = customerList.stream()
    .collect(Collectors.collectingAndThen(
        Collectors.toSet(),
        set -> set.stream().map(Customer::getEmail).collect(Collectors.toList())));
```

**Use Case:** Deduplicate customers and convert to a list of emails for promotional campaigns.

---

## mapping with downstream collector

The `mapping` method applies a mapping function to elements in a stream and collects the results using another collector.

**Return Type:** `Collector<T, A, R>` that applies a mapping function and collects the results.

**Example:**

**Question:** Collect the lengths of all strings in a list and sum them.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
int totalLength = words.stream()
                       .collect(Collectors.mapping(String::length, Collectors.summingInt(Integer::intValue)));
System.out.println(totalLength);
```

**Output:**

```
17
```

**Real-time Use Case:**

Collect all unique product names from a list of orders.

```java
Set<String> uniqueProductNames = orderList.stream()
    .flatMap(order -> order.getProducts().stream())
    .collect(Collectors.mapping(Product::getName, Collectors.toSet()));
```

**Use Case:** Generate a list of unique product names for inventory analysis or product filters.

---

## toMap

The `toMap` method in Java Streams converts the elements of a stream into a `Map` using key and value mapping functions.

**Return Type:** `Map<K, V>` where `K` is the key type and `V` is the value type.

**Example:**

**Question:** Convert a list of strings into a map where the key is the string and the value is its length.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
Map<String, Integer> map = words.stream()
                                .collect(Collectors.toMap(Function.identity(), String::length));
System.out.println(map);
```

**Output:**

```
{apple=5, banana=6, cherry=6}
```

**Real-time Use Case:**

Create a map where each order ID is associated with its total amount.

```java
Map<Long, Integer> orderAmountMap = orderList.stream()
    .collect(Collectors.toMap(Order::getId, Order::getTotalAmount));
```

**Use Case:** Quickly retrieve the total amount of an order by ID for lookup or reconciliation.

---

## toConcurrentMap

The `toConcurrentMap` method is similar to `toMap`, but produces a `ConcurrentMap` for thread-safe operations in concurrent environments.

**Return Type:** `ConcurrentMap<K, V>` where `K` is the key type and `V` is the value type.

**Example:**

**Question:** Convert a list of strings into a concurrent map where the key is the string and the value is its length.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
ConcurrentMap<String, Integer> map = words.stream()
                                          .collect(Collectors.toConcurrentMap(Function.identity(), String::length));
System.out.println(map);
```

**Output:**

```
{apple=5, banana=6, cherry=6}
```

---

## reducing

The `reducing` method in Java Streams performs a reduction on the elements of a stream using an associative accumulation function.

**Arguments:**
- **Identity Value (optional):** A starting value, used as the default when the stream is empty.
- **Binary Operator:** A function that combines two arguments into a result.

**Return Type:** `Optional<T>` if no identity is provided, or `T` if an identity is provided.

**Example:**

**Question:** Find the sum of a list of integers.

**Solution:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream()
                 .collect(Collectors.reducing(0, Integer::sum));
System.out.println(sum);
```

**Output:**

```
15
```

**Real-time Use Case:**

Sum up the total revenue from a list of orders.

```java
int totalRevenue = orderList.stream()
    .map(Order::getTotalAmount)
    .collect(Collectors.reducing(0, Integer::sum));
```

**Use Case:** Calculate total revenue for financial reporting over a period.

---

## flatMapping

The `flatMapping` method flattens a stream of collections and applies a collector to the flattened elements.

**Return Type:** `Collector` that applies a flat-mapping function and collects the results.

**Example:**

**Question:** Flatten a list of lists of integers and collect the result as a single list.

**Solution:**

```java
List<List<Integer>> listOfLists = Arrays.asList(
    Arrays.asList(1, 2, 3),
    Arrays.asList(4, 5, 6),
    Arrays.asList(7, 8, 9)
);
List<Integer> flattenedList = listOfLists.stream()
                                         .collect(Collectors.flatMapping(Collection::stream, Collectors.toList()));
System.out.println(flattenedList);
```

**Output:**

```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Real-time Use Case:**

Create a single list of all products across all orders.

```java
List<Product> allProducts = orderList.stream()
    .collect(Collectors.flatMapping(
        order -> order.getProducts().stream(),
        Collectors.toList()
    ));
```

**Use Case:** Aggregate products for a complete catalog or inventory analysis.

---

## summarizingDouble

The `summarizingDouble` method generates summary statistics for a stream of double values.

**Return Type:** `DoubleSummaryStatistics` object containing the summary statistics.

**Example:**

**Question:** Generate summary statistics (count, sum, min, average, max) for a list of double values.

**Solution:**

```java
List<Double> numbers = Arrays.asList(1.5, 2.5, 3.5, 4.5, 5.5);
DoubleSummaryStatistics stats = numbers.stream()
                                       .collect(Collectors.summarizingDouble(Double::doubleValue));
System.out.println(stats);
```

**Output:**

```
DoubleSummaryStatistics{count=5, sum=17.5, min=1.5, average=3.500000, max=5.5}
```

---

## summarizingLong

The `summarizingLong` method generates summary statistics for a stream of long values.

**Return Type:** `LongSummaryStatistics` object containing the summary statistics.

**Example:**

**Question:** Generate summary statistics (count, sum, min, average, max) for a list of long values.

**Solution:**

```java
List<Long> numbers = Arrays.asList(10L, 20L, 30L, 40L, 50L);
LongSummaryStatistics stats = numbers.stream()
                                     .collect(Collectors.summarizingLong(Long::longValue));
System.out.println(stats);
```

**Output:**

```
LongSummaryStatistics{count=5, sum=150, min=10, average=30.000000, max=50}
```

---

## groupingByConcurrent

The `groupingByConcurrent` method is similar to `groupingBy`, but returns a `ConcurrentMap` for thread-safe operations.

**Return Type:** `ConcurrentMap<K, List<T>>` where `K` is the type of the classifier.

**Example:**

**Question:** Group a list of strings by their length in a thread-safe manner.

**Solution:**

```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "date");
ConcurrentMap<Integer, List<String>> groupedByLength = words.stream()
                                                            .collect(Collectors.groupingByConcurrent(String::length));
System.out.println(groupedByLength);
```

**Output:**

```
{4=[date], 5=[apple], 6=[banana, cherry]}
```

---

## teeing

The `teeing` method in Java Streams combines two collectors into one, merging their results into a final output.

**Return Type:** `Collector<T, ?, R>` that combines the results of two collectors.

**Example:**

**Question:** Compute both the sum and the count of a list of integers and return the result as a map.

**Solution:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
Map<String, Integer> result = numbers.stream()
    .collect(Collectors.teeing(
        Collectors.summingInt(Integer::intValue),
        Collectors.counting(),
        (sum, count) -> Map.of("sum", sum, "count", count.intValue())
    ));
System.out.println(result);
```

**Output:**

```
{sum=15, count=5}
```

---

