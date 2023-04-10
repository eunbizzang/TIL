https://api.jquery.com/jquery.getjson/

This is a shorthand Ajax function, which is equivalent to:

```
$.ajax({
  dataType: "json",
  url: url,
  data: data,
  success: success
});
```


Load the JSON data from test.js and access a name from the returned JSON data.

```
$.getJSON( "test.js", function( json ) {
  console.log( "JSON Data: " + json.users[ 3 ].name );
 });
```


Load the JSON data from test.js, passing along additional data, and access a name from the returned JSON data. If an error occurs, log an error message instead.

```
$.getJSON( "test.js", { name: "John", time: "2pm" } )
  .done(function( json ) {
    console.log( "JSON Data: " + json.users[ 3 ].name );
  })
  .fail(function( jqxhr, textStatus, error ) {
    var err = textStatus + ", " + error;
    console.log( "Request Failed: " + err );
});
```