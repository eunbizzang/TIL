Referenced :
https://theprogrammersfirst.blogspot.com/2020/06/hibernate-jpa-notfound-example.html


@NotFound
The @NotFound annotation is used to specify the NotFoundAction strategy for when an element is not found in a given association.


1. EXCEPTION
An exception is thrown when an element is not found (default and recommended).

2. IGNORE
Ignore the element when not found in the database.


@NotFound association mapping
When dealing with associations which are not enforced by a Foreign Key, it’s possible to bump into inconsistencies if the child record cannot reference a parent entity.

By default, Hibernate will complain whenever a child association references a non-existing parent record. However, you can configure this behavior so that Hibernate can ignore such an Exception and simply assign null as a parent object referenced.

To ignore non-existing parent entity references, even though not really recommended, it’s possible to use the annotation org.hibernate.annotation.NotFound annotation with a value of org.hibernate.annotations.NotFoundAction.IGNORE.


The @ManyToOne and @OneToOne associations that are annotated with @NotFound(action = NotFoundAction.IGNORE) are always fetched eagerly even if the fetch strategy is set to FetchType.LAZY.



```ex.java
//Example : @NotFound mapping example
@Entity
@Table( name = "Person" )
public static class Person {

 @Id
 private Long id;

 private String name;

 private String cityName;

 @ManyToOne
 @NotFound ( action = NotFoundAction.IGNORE )
 @JoinColumn(
  name = "cityName",
  referencedColumnName = "name",
  insertable = false,
  updatable = false
 )
 private City city;

 //Getters and setters are omitted for brevity

}
```
```
@Entity
@Table( name = "City" )
public static class City implements Serializable {

 @Id
 @GeneratedValue
 private Long id;

 private String name;

 //Getters and setters are omitted for brevity

}
```


https://stackoverflow.com/questions/13539050/entitynotfoundexception-in-hibernate-many-to-one-mapping-however-data-exist






https://stackoverflow.com/questions/67135564/how-to-make-a-field-as-optional-in-a-jpa-entity
