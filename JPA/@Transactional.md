Reference:
https://www.baeldung.com/transaction-configuration-with-jpa-and-spring
https://javarevisited.blogspot.com/2021/08/spring-transactional-example-how-to.html#axzz7Wl48Baky

What does @transactional annotation do?

The @Transactional annotation makes use of the attributes rollbackFor or rollbackForClassName to rollback the transactions, and the attributes noRollbackFor or noRollbackForClassName to avoid rollback on listed exceptions. The default rollback behavior in the declarative approach will rollback on runtime exceptions.


What is @transactional annotation in Java?

Transactional annotation provides the application the ability to declaratively control transaction boundaries on CDI managed beans, as well as classes defined as managed beans by the Java EE specification, at both the class and method level where method level annotations override those at the class level.


What does @transactional annotation do in Spring?

One of the most essential parts of Spring MVC is the @Transactional annotation, which provides broad support for transaction management and allows developers to concentrate on business logic rather than worrying about data integrity in the event of system failures.


Some of the main benefits that can be obtained through transaction management are,

1. TransactionTemplate or PlatformTransactionManager implementations are used to support programmatic transaction management.

2. You can use JDBC, Hibernate, Spring Data JPA, JDO, JTA, and others.

3. Can be used in declarative transaction management. Spring uses AOP (Aspect Orient Programming) over the transactional methods to provide data integrity.


A database transaction is a sequence of actions that are treated as a single unit of work. The concepts of transactions can be described with the following four key properties called ACID properties.

1. Atomocity – This refers to either the entire sequence of operation is successful or unsuccessful.

2. Consistency – Consistency of referential integrity of the database.

3. Isolation – There may be many transactions processing with the same data set simultaneously.

4. Durability – Results of the transactions can not be erased from the database due to system failures.


* Read-write and read-only transaction routing in Spring

 1. more common annotation-config
```
@Configuration
@EnableTransactionManagement
public class PersistenceJPAConfig{

@Bean
public PlatformTransactionManager transactionManager(){
    JpaTransactionManager transactionManager = new JpaTransactionManager();
    transactionManager.setEntityManagerFactory(
    entityManagerFactoryBean().getObject() );
    return transactionManager;
}
```

But if you use the Spring boot project with this dependency spring-boot-starter-data-jpa, then transaction management will be enabled by default.


 2. The @Transactional Annotation
You can annotate a bean with @Transactional either at the class or method level.

```
import org.springframework.stereotype.Service;
import javax.transaction.Transactional;

@Service
@Transactional
public class ProductService {

}
```

From the above code, you can see that @Transactional annotation enables,

    1. Rollback rules of the transactions

    2. Transaction should be read-only

    3. Isolation level of the transaction

    4. Timeout of the operation wrapped by transaction


3. Transaction Management in Spring Framework
When it comes to transaction management, there are 2 ways to achieve it. Spring Programmatic transaction management and Spring Declarative transaction management. 

3.1 Spring Programmatic Transaction Management.

Transaction management code needs to be explicitly written, and it is tightly bound to business logic in this case. This allows us to manage the transaction with the help of programming in your source code. That gives you extreme flexibility, but it is difficult to maintain.

```ProgrammaticTransactionManagement.java
StudentTransaction studentTransaction = entityManager.getTransaction();
try {
    studentTransaction.begin(); //start of the first student transaction
   //this is the place that used to create students and link them
  /* register student - query 1
      create student
     link note to the user - query 2 */

    //Commit Student Transaction
      studentTransaction.commit();
    } catch(Exception exception) {
          //Rollback Student Transaction
          userNoteTransaction.rollback();
        throw exception;
}
```

3.2 Spring Declarative Transaction Management

Instead of hard coding in your source code, you can handle the transaction with the help of settings. To manage transactions, you only need to utilize annotations or XML-based settings. This also allows the transaction management and business code to be separated. Some of the steps associated with the declarative transaction are,

1. If the method has been included in the transactional configuration, then the created advice will begin the transaction before calling the method

2. Target method will be executed in a try/catch block.

3. If the method finishes normally, the AOP advice commits the transaction successfully; otherwise, it performs a rollback.
```DeclarativeTransactionManagement.java
@Transactional
public void addStudentToSpecificClass() {
/* register student - query
create new student
link student to class - query 2 */
}
```

Different types of Transaction Propagation in Transaction Management specify whether or not the related component will participate in the transaction and what occurs if the caller component/service has or has not previously created/started a transaction.






