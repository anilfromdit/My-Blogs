---
title: "Best Practices for Using @Transactional in Spring Boot"
seoTitle: "Best Practices for Using Transactional in Spring Boot"
seoDescription: "Transaction management in Spring Boot is crucial for ensuring data integrity and consistency in your applications. The Transaction Manager plays a......"
datePublished: Thu Sep 07 2023 04:30:09 GMT+0000 (Coordinated Universal Time)
cuid: clm8o6ohz000809jj6nrh93ro
slug: best-practices-for-using-transactional-in-spring-boot
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693917655615/28a1eb72-b2e5-42bd-b17a-63daf8900e83.png
tags: programming-blogs, java, best-practices, springboot, transactional

---

![](https://cdn-images-1.medium.com/max/1100/1*e85pmtH-HrHKeLDxqKNEyQ.png align="left")

### Understanding Transaction Management in Spring Boot

Transaction management in Spring Boot is crucial for ensuring data integrity and consistency in your applications. The Transaction Manager plays a pivotal role in managing transactions. Here’s what you need to know:

### Role of TransactionManager

When a method annotated with `@Transactional` is called, Spring Boot utilizes the TransactionManager to create or join a transaction. The Transaction Manager oversees the transaction's lifecycle, including committing or rolling it back based on the outcome of the operation.

### Transaction Isolation Levels

Spring Boot supports various transaction isolation levels, including READ\_UNCOMMITTED, READ\_COMMITTED, REPEATABLE\_READ, and SERIALIZABLE. These levels determine how transactions interact with each other and the underlying data. Choose the right isolation level for your application’s needs.

```java
@Service
public class UserService {
  @Autowired
  private UserRepository userRepository;
jj@Transactional
  public void updateUser(String username, String email) {
    User user = userRepository.findByUsername(username);
    user.setEmail(email);
    // ... other operations
  }
}
```

In the example above, `updateUser()` is marked with `@Transactional`, allowing Spring Boot to manage the transaction's behavior.

### Understanding Transaction Propagation

Transactional behaviour can vary depending on how methods are annotated. Here’s a key distinction:

### @Transactional vs. @Transactional(propagation = Propagation.REQUIRES\_NEW)

* `@Transactional` creates or joins a transaction.
    
* `@Transactional(propagation = Propagation.REQUIRES_NEW)` creates a new transaction, suspending the current one if it exists.
    

```java
@Service
public class MyService {
@Transactional
    public void methodA() {
        // ... some code here
        methodB();
        // ... some code here
    }
@Transactional(propagation = Propagation.REQUIRES_NEW)
    public void methodB() {
        // ... some code here
    }
}
```

In this example, `methodA()` invokes `methodB()`. `methodA()`'s transaction is suspended when `methodB()` begins a new transaction due to the `REQUIRES_NEW` propagation setting.

### Handling Transactions Within the Same Class

Spring’s default behavior when a `@Transactional` method calls another `@Transactional` method within the same class is noteworthy:

### Default Behavior

By default, Spring uses a “proxy-based” approach. If a `@Transactional` method calls another `@Transactional` method within the same class, the transactional behaviour isn't applied.

```java
@Service
public class MyService {
    @Autowired
    private MyService self;
ja   @Transactional
    public void methodA() {
        // ... some code here
        self.methodB();
        // ... some code here
    }
@Transactional
    public void methodB() {
        // ... some code here
    }
}
```

In this example, `methodA()` and `methodB()` are both marked with `@Transactional`. However, due to the "proxy-based" approach, the transactional behaviour isn't applied to `methodB()` when called from `methodA()`. To resolve this, consider AspectJ-based weaving or moving the `@Transactional` method to a separate class.

### Managing Transactions Across Different Beans

When calling a method on a different bean, Spring creates a new proxy around the target bean, allowing it to manage transactional behaviour:

```java
@Service
public class MyService {
@Autowired
    private OtherService otherService;
@Transactional
    public void methodA() {
        // ... some code here
        otherService.methodB();
        // ... some code here
    }
}
@Service
public class OtherService {
   @Transactional
    public void methodB() {
        // ... some code here
    }
}
```

In this example, `methodA()` calls `methodB()` on a different bean (`OtherService`). Spring creates a new proxy around `OtherService` to apply transactional behaviour based on `methodA()`Propagation settings.

### Handling Unchecked Exceptions

When a `@Transactional` method throws an unchecked exception, Spring automatically rolls back the transaction by default. This ensures that data changes within the transaction are not persisted if an error occurs.

```java
@Service
@Transactional
public class UserService {
 @Autowired
  private UserRepository userRepository;
 public void updateUser(String username, String email) {
    User user = userRepository.findByUsername(username);
    if (user == null) {
      throw new RuntimeException("User not found");
    }
    user.setEmail(email);
    userRepository.save(user);
    throw new RuntimeException("Something went wrong");
  }
}
```

In this example, `updateUser()` is marked with `@Transactional` and throws an unchecked exception. The transaction will roll back by default, discarding the changes made to the user's email address.

### Customizing Rollback Behavior

You can customize the rollback behavior using the `rollbackFor` or `noRollbackFor` properties of the `@Transactional` annotation.

```java
@Service
@Transactional(noRollbackFor = RuntimeException.class)
public class UserService { 
// ...
}
```

In this example, we specify that a `RuntimeException` should not trigger a rollback. This can be useful when you want to keep changes within the transaction, even if an error occurs.

### Default Rollback Behavior

By default, a `@Transactional` method rolls back the transaction on any unchecked exception. Customize this behavior using `rollbackFor` or `noRollbackFor` properties.

### Private Methods and @Transactional

`@Transactional` works only on public methods. Spring creates a proxy around public methods to manage transactional behaviour. Private methods are not visible to the proxy and cannot be wrapped in a transactional context.

```java
@Service
public class MyService {
   @Transactional
    public void methodA() {
        // ... some code here
        methodB();
        // ... some code here
    }
    private void methodB() {
        // ... some code here
    }
}
```

In this example, `methodA()` is marked with `@Transactional`, but `methodB()` is not. To enable transactional behaviour for `methodB()`, make it public or move the `@Transactional` annotation to a method that calls both `methodA()` and `methodB()`.

### Handling Concurrency Issues

Spring Boot’s `@Transactional` annotation provides a mechanism for handling concurrency issues by serializing transactions. The default isolation level prevents most concurrency problems by ensuring that transactions do not interfere with each other.

```java
@Service
public class UserService {
  @Autowired
  private UserRepository userRepository;
 @Transactional
  public void updateUser(String username, String email) {
    User user = userRepository.findByUsername(username);
    user.setEmail(email);
    // ... other operations
  }
}
```

In this example, `updateUser()` is marked with `@Transactional`, and Spring ensures that transactions are serialized when multiple threads attempt to modify the same user's email address concurrently. This prevents data inconsistencies and race conditions.

Remember that the default isolation level used by `@Transactional` in Spring is `Isolation.DEFAULT`, which aligns with the underlying data source's default. This typically results in "read committed" isolation, which is suitable for most databases.

Mastering `@Transactional` is crucial for effective transaction management in Spring Boot applications. These best practices will help you handle transactions with confidence and precision.

### Enjoyed This Article?

> *If you enjoy reading this post, got help, and knowledge through it, and want to support my efforts please clap this article and follow.  
> *[*Click Here To Subscribe For Newsletter*](https://blog.anilgulati.tech/newsletter)*To explore more of my work, visit my portfolio at* [*anilgulati.tech*](http://anilgulati.tech?utmSource=hashnode&article=best-practices-for-using-transactional-in-spring-boot)*.*