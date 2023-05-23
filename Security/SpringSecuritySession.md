https://docs.spring.io/spring-session/reference/2.7/spring-security.html

Spring Security Concurrent Session Control

Spring Session provides integration with Spring Security to support its concurrent session control. 
This allows limiting the number of active sessions that a single user can have concurrently, 
but, unlike the default Spring Security support, this also works in a clustered environment. 
This is done by providing a custom implementation of Spring Security’s SessionRegistry interface.

When using Spring Security’s Java config DSL, you can configure the custom SessionRegistry through the SessionManagementConfigurer, 
as the following listing shows:

```
@Configuration
public class SecurityConfiguration<S extends Session> extends WebSecurityConfigurerAdapter {

	@Autowired
	private FindByIndexNameSessionRepository<S> sessionRepository;

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
			// other config goes here...
			.sessionManagement((sessionManagement) -> sessionManagement
				.maximumSessions(2)
				.sessionRegistry(sessionRegistry())
			);
	}

	@Bean
	public SpringSessionBackedSessionRegistry<S> sessionRegistry() {
		return new SpringSessionBackedSessionRegistry<>(this.sessionRepository);
	}

}
```

This assumes that you have also configured Spring Session to provide a FindByIndexNameSessionRepository that returns Session instances.

When using XML configuration, it would look something like the following listing:


```
<security:http>
	<!-- other config goes here... -->
	<security:session-management>
		<security:concurrency-control max-sessions="2" session-registry-ref="sessionRegistry"/>
	</security:session-management>
</security:http>

<bean id="sessionRegistry"
	  class="org.springframework.session.security.SpringSessionBackedSessionRegistry">
	<constructor-arg ref="sessionRepository"/>
</bean>
```
This assumes that your Spring Session SessionRegistry bean is called sessionRegistry, 
which is the name used by all SpringHttpSessionConfiguration subclasses.

