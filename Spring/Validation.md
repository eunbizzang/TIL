https://www.baeldung.com/javax-validation
https://www.baeldung.com/spring-boot-bean-validation

https://www.baeldung.com/spring-service-layer-validation
https://reflectoring.io/bean-validation-with-spring-boot/

https://www.baeldung.com/spring-boot-bean-validation


### Validation in Spring Boot
In POST and PUT requests, it’s common to pass a JSON payload within the request body. Spring automatically maps the incoming JSON to a Java object.
```
class Input {

  @Min(1)
  @Max(10)
  private int numberBetweenOneAndTen;

  @Pattern(regexp = "^[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}$")
  private String ipAddress;
  
  // ...
}
```
To validate the request body of an incoming HTTP request, we annotate the request body with the @Valid annotation in a REST controller:
```
@RestController
class ValidateRequestBodyController {

  @PostMapping("/validateBody")
  ResponseEntity<String> validateBody(@Valid @RequestBody Input input) {
    return ResponseEntity.ok("valid");
  }

}
```

### Using Validation Groups to Validate Objects Differently for Different Use Cases
```
interface OnCreate {}

interface OnUpdate {}

```

```
class InputWithGroups {

  @Null(groups = OnCreate.class)
  @NotNull(groups = OnUpdate.class)
  private Long id;
  
  // ...
  
}
```

Spring supports validation groups with the @Validated annotation:
```
@Service
@Validated
class ValidatingServiceWithGroups {

    @Validated(OnCreate.class)
    void validateForCreate(@Valid InputWithGroups input){
      // do something
    }

    @Validated(OnUpdate.class)
    void validateForUpdate(@Valid InputWithGroups input){
      // do something
    }

}
```











