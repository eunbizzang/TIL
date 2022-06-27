Referenced:
https://www.baeldung.com/java-optional-return


The Optional type was introduced in Java 8.  
It provides a clear and explicit way to convey the message that there may not be a value, without using null.

* Optional as Return Type

Most of the time, returning an Optional is just fine:
```
public static Optional<User> findUserByName(String name) {
    User user = usersByName.get(name);
    Optional<User> opt = Optional.ofNullable(user);
    return opt;
}

```
we can use the Optional API in the calling method:


```
public static void changeUserName(String oldFirstName, String newFirstName) {
    findUserByFirstName(oldFirstName).ifPresent(user -> user.setFirstName(newFirstName));
}
```
static method or utility method to return an Optional value.  



However, there are many situations where we should not return an Optional type.


Many times, it's just simply better to return the actual type rather than an Optional type.
1. Serialization
```
public class Sock implements Serializable {
    Integer size;
    Optional<Sock> pair;

    // ... getters and setters
}
```
If we were to try and serialize this, we'd get an NotSerializableException:


```
new ObjectOutputStream(new ByteArrayOutputStream()).writeObject(new Sock());
```
Also, it certainly adds what may be unnecessary complexity.


2. JSON
Modern applications convert Java objects to JSON all the time. If a getter returns an Optional type, we'll most likely see some unexpected data structure in the final JSON.
```
private String firstName;

public Optional<String> getFirstName() {
    return Optional.ofNullable(firstName);
}

public void setFirstName(String firstName) {
    this.firstName = firstName;
}


//So, if we use Jackson to serialize an instance of Optional, we'll get:

{"firstName":{"present":true}}


//But, what we'd really want is:

{"firstName":"Baeldung"}
```


3. JPA
 cousin to serialization: writing data to a database


```
@Entity
public class UserOptionalField implements Serializable {
    @Id
    private long userId;

    private Optional<String> firstName;

    // ... getters and setters
}


//And if we try to persist it:

UserOptionalField user = new UserOptionalField();
user.setUserId(1l);
user.setFirstName(Optional.of("Baeldung"));
entityManager.persist(user);

// Sadly, we run into an error:
```

4. Expression Languages (Front-end)
Preparing a DTO for the front-end presents similar difficulties.

```
<c:out value="${requestScope.user.firstName}" />
```

```
// Since it's an Optional, we'll not see “Baeldung“. Instead, we'll see the String representation of the Optional type:
Optional[Baeldung]
```