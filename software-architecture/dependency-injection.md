# Dependency Injection

> [!Note]
> The example is demonstrated using java and it applies for all object-oriented languages.

Traditionally the object creation in java is done by using the new keyword.

```java
Object object = new Object();
```

When you, as a developer, are responsible for creating an object, you must also maintain its lifecycle, including 
updating, destroying, etc. But have you ever explicitly destroyed an object? Probably not.

This is where Inversion of Control (IoC) comes into the picture. Instead of you having control (responsibility) over an 
object’s lifecycle, IoC shifts this control to someone else—usually a framework.

### Inversion of Control (IoC)

IoC is a SOLID principle that states a framework takes control over the flow of code, rather than following the 
traditional procedural flow. IoC states that a software component should receive its dependencies from an external 
source rather than creating them internally. This decouples components, making the system more flexible, reusable, and 
testable.

By utilizing IoC, developers write more loosely coupled code, which results in a more maintainable and extensible system.

### Dependency Injection (DI)

**Dependency Injection (DI)** is a software design pattern that implements IoC. DI makes classes independent of their
dependencies by providing those dependencies externally. This can be achieved via:
- Constructor Injection
- Setter Injection
- Field Injection

**Without Dependency Injection**

In this scenario, the UserService class is responsible for creating its own UserRepository,
which tightly couples these two classes.

```java
public class UserService {
    private UserRepository userRepository;

    public UserService() {
        this.userRepository = new UserRepository();
    }

    public void saveUser(User user) {
        userRepository.save(user);
    }
}
```

**With Dependency Injection**

By using Dependency Injection, UserRepository is provided externally, making UserService more flexible and testable.
The class is no longer responsible for creating its dependencies.

```java
// UserService.java
public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void saveUser(User user) {
        userRepository.save(user);
    }
}

//AuthenticationService.java
public class AuthenticationService {
    private final UserRepository userRepository;
		
    public AuthenticationService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    
    //.... methods
}


// Main.java
class Main {
    public static void main(String[] args) {
        private UserRepository userRepository = new UserRepository();
        private AuthenticationService authService = new AuthenticationService(userRepository);
        private UserService userService = new UserService(userRepository);
    }
}
```
Therefore, Dependency Injection, as part of the Inversion of Control principle, helps decouple classes, making them
easier to manage and test. By injecting dependencies, the class no longer creates its own dependencies, allowing more
flexibility in how objects are constructed and managed.

This design pattern is essential for building maintainable, extensible, and testable software.

