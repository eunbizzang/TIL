https://www.baeldung.com/spring-boot-internationalization

Let's add a drop-down to our HTML page with the two locales whose names are also localized in our properties files:
```
<span th:text="#{lang.change}"></span>:
<select id="locales">
    <option value=""></option>
    <option value="en" th:text="#{lang.eng}"></option>
    <option value="fr" th:text="#{lang.fr}"></option>
</select>
```
Then we can add a jQuery script that will call the /international URL with the respective lang parameter, depending on which drop-down option the user selects:

```
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js">
</script>
<script type="text/javascript">
$(document).ready(function() {
    $("#locales").change(function () {
        var selectedOption = $('#locales').val();
        if (selectedOption != ''){
            window.location.replace('international?lang=' + selectedOption);
        }
    });
});
</script>
```
