Reference
: https://www.baeldung.com/jpa-composite-primary-keys

Composite Primary Keys
A composite primary key, also called a composite key, is a combination of two or more columns to form a primary key for a table.
*The composite primary key class must be public.
*It must have a no-arg constructor.
*It must define the equals() and hashCode() methods.
*It must be Serializable.


1. The IdClass Annotation

```AccountId.java
public class AccountId implements Serializable {
    private String accountNumber;

    private String accountType;

    // default constructor

    public AccountId(String accountNumber, String accountType) {
        this.accountNumber = accountNumber;
        this.accountType = accountType;
    }

    // equals() and hashCode()
}
```
We must also declare the fields from the AccountId class in the entity Account and annotate them with @Id.


```Account.java
@Entity
@IdClass(AccountId.class)
public class Account {
    @Id
    private String accountNumber;

    @Id
    private String accountType;

    // other fields, getters and setters
}
```

The composite primary key class must be public, contains a no-argument constructor, defines both equals() and hashCode() methods, and implements the Serializable interface.

2. The EmbeddedId Annotation
@EmbeddedId is an alternative to the @IdClass annotation.
the primary key class, BookId, must be annotated with @Embeddable:

```BookId.java
@Embeddable
public class BookId implements Serializable {
    private String title;
    private String language;

    // default constructor

    public BookId(String title, String language) {
        this.title = title;
        this.language = language;
    }

    // getters, equals() and hashCode() methods
}
```
Then we need to embed this class in the Book entity using @EmbeddedId:

```Book.java
@Entity
public class Book {
    @EmbeddedId
    private BookId bookId;

    // constructors, other fields, getters and setters
}
```



For example, these different structures affect the JPQL queries that we write.

With @IdClass, the query is a bit simpler
```
SELECT account.accountNumber FROM Account account
```


With @EmbeddedId, we have to do one extra traversal:
```
SELECT book.bookId.title FROM Book book
```


Also, @IdClass can be quite useful in places where we are using a composite key class that we can't modify.
If we're going to access parts of the composite key individually, we can make use of @IdClass, but in places where we frequently use the complete identifier as an object, @EmbeddedId is preferred.