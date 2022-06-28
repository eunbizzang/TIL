https://www.baeldung.com/jpa-attribute-converters

the usage of the Attribute Converters available in JPA 2.1 – which, simply put, allow us to map JDBC types to Java classes.



```PersonName.java
public class PersonName implements Serializable {

    private String name;
    private String surname;

    // getters and setters
}
```


@PersonName to an @Entity class:
```Person.java
@Entity(name = "PersonTable")
public class Person {
   
    private PersonName personName;

    //...
}
```

we have to annotate our converter class with @Converter and implement the AttributeConverter interface
```
@Converter
public class PersonNameConverter implements 
  AttributeConverter<PersonName, String> {

    private static final String SEPARATOR = ", ";

    @Override
    public String convertToDatabaseColumn(PersonName personName) {
        if (personName == null) {
            return null;
        }

        StringBuilder sb = new StringBuilder();
        if (personName.getSurname() != null && !personName.getSurname()
            .isEmpty()) {
            sb.append(personName.getSurname());
            sb.append(SEPARATOR);
        }

        if (personName.getName() != null 
          && !personName.getName().isEmpty()) {
            sb.append(personName.getName());
        }

        return sb.toString();
    }

    @Override
    public PersonName convertToEntityAttribute(String dbPersonName) {
        if (dbPersonName == null || dbPersonName.isEmpty()) {
            return null;
        }

        String[] pieces = dbPersonName.split(SEPARATOR);

        if (pieces == null || pieces.length == 0) {
            return null;
        }

        PersonName personName = new PersonName();        
        String firstPiece = !pieces[0].isEmpty() ? pieces[0] : null;
        if (dbPersonName.contains(SEPARATOR)) {
            personName.setSurname(firstPiece);

            if (pieces.length >= 2 && pieces[1] != null 
              && !pieces[1].isEmpty()) {
                personName.setName(pieces[1]);
            }
        } else {
            personName.setName(firstPiece);
        }

        return personName;
    }
}
```





