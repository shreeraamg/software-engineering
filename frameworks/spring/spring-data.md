# Spring Data

- A framework from the Spring Ecosystem.
- Simplifies interaction with various datasource technologies, both relational and non-relational.
- Goal is to reduce boilerplate code required for data access by providing a consistent, high-level abstraction for data repositories.

### Key Concepts

- **Repository Abstraction** - No need of writing actual implementation code. Spring automatically provides implementation based on the interface definitions.
- **Consistency Across Data stores** - The same repository interfaces and query methods apply across different data stores irrespective of JPA, MongoDB, Neo4j or Elasticsearch.
- **Derived Queries** - Defining methods that follow specific conventions will create query behind the scenes by Spring Data.

### Read Also

- [Spring Data JPA](spring-data-jpa.md)
- [Repository Interfaces](repository-interfaces.md)