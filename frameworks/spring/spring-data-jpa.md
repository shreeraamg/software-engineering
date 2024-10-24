# Spring Data JPA

A module inside the Spring Data that provides abstraction for working with relational databases using the Jakarta Persistence API (JPA). JPA makes it easier to interact with databases using object-relational mapping (ORM).

### Key Concepts

**JPA Integration** 

- JPA is a specification for ORM in Java that allows mapping Java objects (entities) with database tables and handle CRUD Operations.
- Spring Data JPA simplifies working with JPA by abstracting away common tasks, like creating entity manager factories, transaction handling, and query generation.

**Repository Pattern**

- It provides the `JpaRepository` interface, which extends Spring Data’s repository abstraction with additional methods for JPA-specific tasks, such as batch updates, flushing, and handling the persistence context.

**Entity Management**

- It allows defining entities using JPA annotations like `@Entity`, `@Id`, `@OneToMany`, and `@ManyToOne`, which map Java classes and relationships to database tables and columns.
- Spring Data JPA helps you manage the lifecycle of these entities without requiring you to write verbose JDBC code.

**Custom Queries**

- Spring Data JPA allows you to define custom JPQL (Java Persistence Query Language) queries using the `@Query` annotation or native SQL queries for more complex data access scenarios.

**Pagination & Sorting**

- Besides basic CRUD operations, Spring Data JPA provides built-in support for pagination (Pageable) and sorting (Sort), which is essential for handling large datasets efficiently.

### Basic Example of Spring Data JPA

```java
@Repository
public interface UserRepository extends JpaRepository<User, Integer> {
    List<User> findByLastName(String lastName);
}
```

### Read Also

- [Repository Interfaces](repository-interfaces.md)