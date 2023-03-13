https://www.baeldung.com/jpa-entities

The Transient Annotation
Sometimes, we may want to make a field non-persistent. We can use the @Transient annotation to do so. It specifies that the field won't be persisted.

For instance, we can calculate the age of a student from the date of birth.

So let's annotate the field age with the @Transient annotation:

```
@Entity
@Table(name="STUDENT")
public class Student {
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private Long id;
    
    @Column(name="STUDENT_NAME", length=50, nullable=false)
    private String name;
    
    @Transient
    private Integer age;
    
    // other fields, getters and setters
}
```