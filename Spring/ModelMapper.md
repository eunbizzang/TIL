Reference :
https://www.baeldung.com/entity-to-and-from-dto-for-a-java-spring-application


the conversions that need to happen between the internal entities of a Spring application and the external DTOs (Data Transfer Objects) that are published back to the client.


* Model Mapper
is the main library to perform entity-DTO conversion.

```dependency_in_pom.xml
<!-- ModelMapper -->
        <dependency>
            <groupId>org.modelmapper</groupId>
            <artifactId>modelmapper</artifactId>
            <version>2.4.5</version>
        </dependency>
        <!-- ModelMapper end -->
```
