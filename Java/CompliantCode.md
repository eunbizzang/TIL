

Compliant Solution
```
public String getReadableStatus(Job j) {
  if (j.isRunning()) {
    return "Running";
  }
  return j.hasErrors() ? "Failed" : "Succeeded";
}
```

Noncompliant Code Example
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

Noncompliant Code Example
```
public void doSomething(int my_param) {
  int LOCAL;
  ...
}
```