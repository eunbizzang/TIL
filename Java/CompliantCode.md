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