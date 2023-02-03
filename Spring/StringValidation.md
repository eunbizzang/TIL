https://stackoverflow.com/questions/3732809/how-can-a-string-be-validated-in-java


String Example
```
// You can use this pattern:
String regex = "^[a-zA-Z]+$";
if (str.matches(regex)) { 
    // ...
}
```

Email Example
```
String regex = "\\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\\.[A-Z]{2,4}\\b";
if (str.matches(regex)) { 
    // ...
}
```