Reference
: https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.custom-implementations

Custom Implementations for Spring Data Repositories


Spring Data provides various options to create query methods with little coding. 
But when those options don’t fit your needs you can also provide your own custom implementation for repository methods. 


Customizing Individual Repositories
To enrich a repository with custom functionality, you must first define a fragment interface and an implementation for the custom functionality, as follows:

Example 29. Interface for custom repository functionality
```
interface CustomizedUserRepository {
  void someCustomMethod(User user);
}
```

Example 30. Implementation of custom repository functionality
```
class CustomizedUserRepositoryImpl implements CustomizedUserRepository {

  public void someCustomMethod(User user) {
    // Your custom implementation
  }
}
```
The implementation itself does not depend on Spring Data and can be a regular Spring bean.Consequently, you can use standard dependency injection behavior to inject references to other beans (such as a JdbcTemplate), take part in aspects, and so on.
Then you can let your repository interface extend the fragment interface, as follows:

Example 31. Changes to your repository interface
```
interface UserRepository extends CrudRepository<User, Long>, CustomizedUserRepository {

  // Declare query methods here
}
```

Extending the fragment interface with your repository interface combines the CRUD and custom functionality and makes it available to clients.

