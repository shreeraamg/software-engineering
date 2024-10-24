# Repository Interfaces

### Repository

- Marker Interface, part of Spring Data infrastructure.
- It's a core interface of Spring Data and all modules like Spring Data JPA, Spring Data MongoDB uses this interface.
- It's not used directly in most cases. Interfaces like `CrudRepository` or `JpaRepository` are used.

### Crud Repository

- Provides basic CRUD operations on Entities.
- A simpler and fundamental repository interface.
- Return Types
  - Single Entities - `Optional<T>`
  - Collection - `Iterable<T>`

| Operation | Method | Description |
|-|-|-|
|Create|`save(S entity)`|Saves a given entity (creates or updates if it already exists).|
|Read (Find All)|`findAll()`|Returns all entities of the type.|
|Read (By ID)|`findById(ID id)`|Returns the entity with the given ID.|
|Update|`save(S entity)`|The same method used for create will also update if the entity exists.|
|Delete|`deleteById(ID id)`|Deletes the entity with the given ID.|
|Delete (Entity)|`delete(S entity)`|Deletes a given entity.|
|Exists By ID|`existsById(ID id)`|Checks if an entity with the given ID exists.|
|Count|`count()`|Returns the total number of entities.|


### List Repository

- A new interface added in Spring Data 3.0
- Built on top of `CrudRepository`
- Same as Crud Repository but returns `List<T>` over `Iterable<T>` when dealing with collection of entities.

### PagingAndSortingRepository

- An extension of `CrudRepository` with additional methods to retrieve entities using pagination and sorting.
- **Pagination**
  - Allows retrieval of data in chunks (pages) instead of loading all data at once. This is useful when handling large datasets.
  - Method for Pagination
    - `Page<T> findAll(Pageable pageable)` Returns a Page object that contains paginated list of Entities
    - The `Pageable` parameter allows you to specify the page number, size (number of records per page), and sorting options.

```java
// Fetches first 10 users
Page<User> users = userRepository.findAll(PageRequest.of(0, 10));
```

- **Sorting**
  - Enables sorting of query results based on one or more properties.
  - Method for Sorting
    - `Iterable<T> findAll(Sort sort)` This method returns a sorted list of entities.
    - `Sort` parameter allows specifying the properties to sort by and the sort direction (ascending/descending).

```java
// Fetches users sorted by lastName in ascending order
List<User> users = userRepository.findAll(Sort.by("lastName").ascending());
```

- **Pagination with Sorting**
  - `Pageable` object can be used to combine both pagination & sorting.

```java
// Fetches first 10 users sorted by last name in ascending order
Page<User> users = userRepository.findAll(
  PageRequest.of(0, 10, Sort.by("lastName").ascending())
);
```

### JpaRepository

- An extension of `PagingAndSortingRepository` and `CrudRepository` along with JPA specific functionality.
- Methods
  - All CRUD operations
  - Pagination and sorting
  - flushing data and batch operations