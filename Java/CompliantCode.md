

#### Compliant Solution
```
public String getReadableStatus(Job j) {
  if (j.isRunning()) {
    return "Running";
  }
  return j.hasErrors() ? "Failed" : "Succeeded";
}
```

#### Noncompliant Code Example
```
public String getReadableStatus(Job j) {
  return j.isRunning() ? "Running" : j.hasErrors() ? "Failed" : "Succeeded";  // Noncompliant
}
```


### Regular Expression

#### Compliant Solution
```
public void doSomething(int myParam) {
  int local;
  ...
}
```

#### Noncompliant Code Example
```
public void doSomething(int my_param) {
  int LOCAL;
  ...
}
```

### Strings should not be concatenated using '+' in a loop
Strings are immutable objects, so concatenation doesn't simply add the new String to the end of the existing string. Instead, in each loop iteration, the first String is converted to an intermediate object type, the second string is appended, and then the intermediate object is converted back to a String. Further, performance of these intermediate operations degrades as the String gets longer. Therefore, the use of StringBuilder is preferred.

#### Compliant Solution
```
StringBuilder bld = new StringBuilder();
  for (int i = 0; i < arrayOfStrings.length; ++i) {
    bld.append(arrayOfStrings[i]);
  }
  String str = bld.toString();
```

#### Noncompliant Code Example
```
String str = "";
for (int i = 0; i < arrayOfStrings.length ; ++i) {
  str = str + arrayOfStrings[i];
}
```