https://www.w3schools.com/jquery/ajax_param.asp

```
personObj = new Object();
  personObj.firstname = "John";
  personObj.lastname = "Doe";
  personObj.age = 50;
  personObj.eyecolor = "blue"; 

$("div").text($.param(personObj));
```

-> firstname=John&lastname=Doe&age=50&eyecolor=blue