How to check if session exists or not?

```
 HttpSession session = request.getSession();
if (session.isNew()) {
  // Freshly created.
} else {
  // Already created.
}
```
