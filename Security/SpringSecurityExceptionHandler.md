https://www.baeldung.com/spring-security-exceptionhandler

Spring security core exceptions such as AuthenticationException and AccessDeniedException are runtime exceptions. Since these exceptions are thrown by the authentication filters behind the DispatcherServlet and before invoking the controller methods, @ControllerAdvice won't be able to catch these exceptions.
Spring security exceptions can be directly handled by adding custom filters and constructing the response body.
To handle these exceptions at a global level via @ExceptionHandler and @ControllerAdvice, we need a custom implementation of AuthenticationEntryPoint.
