Link : https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#spring-web

@RequestParam

You can use the @RequestParam annotation to bind Servlet request parameters (that is, query parameters or form data) to a method argument in a controller.
example/type=x&name=x

```ex.java
@Controller
@RequestMapping("/pets")
public class EditPetForm {

    // ...

    @GetMapping
    public String setupForm(@RequestParam("petId") int petId, Model model) { 
        Pet pet = this.clinic.loadPet(petId);
        model.addAttribute("pet", pet);
        return "petForm";
    }

    // ...

}
```
By default, method parameters that use this annotation are required, but you can specify that a method parameter is optional by setting the @RequestParam annotation’s required flag to false or by declaring the argument with an java.util.Optional wrapper.



URI patterns

@RequestMapping methods can be mapped using URL patterns. There are two alternatives:

PathPattern — a pre-parsed pattern matched against the URL path also pre-parsed as PathContainer. Designed for web use, this solution deals effectively with encoding and path parameters, and matches efficiently.

AntPathMatcher — match String patterns against a String path. This is the original solution also used in Spring configuration to select resources on the classpath, on the filesystem, and other locations. It is less efficient and the String path input is a challenge for dealing effectively with encoding and other issues with URLs.

PathPattern is the recommended solution for web applications and it is the only choice in Spring WebFlux. Prior to version 5.3, AntPathMatcher was the only choice in Spring MVC and continues to be the default. However PathPattern can be enabled in the MVC config.

PathPattern supports the same pattern syntax as AntPathMatcher. In addition it also supports the capturing pattern, e.g. {*spring}, for matching 0 or more path segments at the end of a path. PathPattern also restricts the use of ** for matching multiple path segments such that it’s only allowed at the end of a pattern. This eliminates many cases of ambiguity when choosing the best matching pattern for a given request. For full pattern syntax please refer to PathPattern and AntPathMatcher.

Some example patterns:

"/resources/ima?e.png" - match one character in a path segment

"/resources/*.png" - match zero or more characters in a path segment

"/resources/**" - match multiple path segments

"/projects/{project}/versions" - match a path segment and capture it as a variable

"/projects/{project:[a-z]+}/versions" - match and capture a variable with a regex

Captured URI variables can be accessed with @PathVariable. For example:

```ex.java
@GetMapping("/owners/{ownerId}/pets/{petId}")
public Pet findPet(@PathVariable Long ownerId, @PathVariable Long petId) {
    // ...
}
```
You can declare URI variables at the class and method levels, as the following example shows:

```ex.java
@Controller
@RequestMapping("/owners/{ownerId}")
public class OwnerController {

    @GetMapping("/pets/{petId}")
    public Pet findPet(@PathVariable Long ownerId, @PathVariable Long petId) {
        // ...
    }
}
```
URI variables are automatically converted to the appropriate type, or TypeMismatchException is raised. Simple types (int, long, Date, and so on) are supported by default and you can register support for any other data type.


@ModelAttribute

You can use the @ModelAttribute annotation on a method argument to access an attribute from the model or have it be instantiated if not present. The model attribute is also overlain with values from HTTP Servlet request parameters whose names match to field names. This is referred to as data binding, and it saves you from having to deal with parsing and converting individual query parameters and form fields. The following example shows how to do so:

```ex.java
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@ModelAttribute Pet pet) {
    // method logic...
}
```
The Pet instance above is sourced in one of the following ways:

>Retrieved from the model where it may have been added by a @ModelAttribute method.

>Retrieved from the HTTP session if the model attribute was listed in the class-level @SessionAttributes annotation.

>Obtained through a Converter where the model attribute name matches the name of a request value such as a path variable or a >request parameter (see next example).

>Instantiated using its default constructor.

>Instantiated through a “primary constructor” with arguments that match to Servlet request parameters. Argument names are >determined through JavaBeans @ConstructorProperties or through runtime-retained parameter names in the bytecode.

One alternative to using a @ModelAttribute method to supply it or relying on the framework to create the model attribute, is to have a Converter<String, T> to provide the instance. This is applied when the model attribute name matches to the name of a request value such as a path variable or a request parameter, and there is a Converter from String to the model attribute type. In the following example, the model attribute name is account which matches the URI path variable account, and there is a registered Converter<String, Account> which could load the Account from a data store:

```ex.java
@PutMapping("/accounts/{account}")
public String save(@ModelAttribute("account") Account account) {
    // ...
}
```
After the model attribute instance is obtained, data binding is applied. The WebDataBinder class matches Servlet request parameter names (query parameters and form fields) to field names on the target Object. Matching fields are populated after type conversion is applied, where necessary. For more on data binding (and validation), see Validation. For more on customizing data binding, see DataBinder.

Data binding can result in errors. By default, a BindException is raised. However, to check for such errors in the controller method, you can add a BindingResult argument immediately next to the @ModelAttribute, as the following example shows:

```ex.java
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@ModelAttribute("pet") Pet pet, BindingResult result) { 
    if (result.hasErrors()) {
        return "petForm";
    }
    // ...
}
```
Adding a BindingResult next to the @ModelAttribute.