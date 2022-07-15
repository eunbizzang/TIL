Authentication

: Verifies you are who you say you are.

* Login form
* Http authentication
* Custom auth, method

Authorization

: Decides if you have permission to access a resource

* Access Control URLs
* Access Control List(ACLs)

---

https://docs.spring.io/spring-security/reference/features/authentication/index.html


Authentication is how we verify the identity of who is trying to access a particular resource. A common way to authenticate users is by requiring the user to enter a username and password. Once authentication is performed we know the identity and can perform authorization.

Authentication Mechanisms
* Username and Password - how to authenticate with a username/password

* OAuth 2.0 Login - OAuth 2.0 Log In with OpenID Connect and non-standard OAuth 2.0 Login (i.e. GitHub)

* Remember Me - how to remember a user past session expiration


Authorization

The advanced authorization capabilities within Spring Security represent one of the most compelling reasons for its popularity. Irrespective of how you choose to authenticate - whether using a Spring Security-provided mechanism and provider, or integrating with a container or other non-Spring Security authentication authority - you will find the authorization services can be used within your application in a consistent and simple way.

