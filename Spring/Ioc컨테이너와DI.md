토비의 스프링 10장

IoC : 오브젝트의 생성, 설정, 사용, 제거 등의 작업을 애플리케이션 코드 대신 독립된 컨테이너가 담당.
Inversion of Control

Ioc를 담당하는 컨테이너를 빈 팩토리 또는 애플리케이션 컨텍스트라고 부름.
오브젝트의 생성과 오브젝트 사이의 런타임 관계를 설정하는 DI 관점으로 볼 때는 컨테이너를 빈 팩토리라고 함.

DI를 위한 빈 팩토리에 엔터프라이즈 애플리케이션을 개발하는데 필요한 여러가지 컨테이너 기능을 추가한 것을 애플리케이션 컨텍스트라고 부름.
즉 애플리케이션 컨텍스트는 그 자체로 IoC와 DI를 위한 빈팩토리 이면서 그 이상의 기능을 가졌다.


* IoC 컨테이너의 종류와 사용 방법

1. StaticApplicationContext
코드를 통해 빈 메타정보를 등록하기 위해 사용
https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/support/StaticApplicationContext.html


ApplicationContext implementation which supports programmatic registration of beans and messages, rather than reading bean definitions from external configuration sources. Mainly useful for testing.


2. GenericApplicationContext
일반적인 애플리케이션 컨텍스트의 구현 클래스
https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/support/GenericApplicationContext.html

Generic ApplicationContext implementation that holds a single internal DefaultListableBeanFactory instance and does not assume a specific bean definition format. Implements the BeanDefinitionRegistry interface in order to allow for applying any bean definition readers to it.
Typical usage is to register a variety of bean definitions via the BeanDefinitionRegistry interface and then call AbstractApplicationContext.refresh() to initialize those beans with application context semantics (handling ApplicationContextAware, auto-detecting BeanFactoryPostProcessors, etc).

In contrast to other ApplicationContext implementations that create a new internal BeanFactory instance for each refresh, the internal BeanFactory of this context is available right from the start, to be able to register bean definitions on it. AbstractApplicationContext.refresh() may only be called once.

스프링 IoC 컨테이너, 즉 애플리케이션 컨텍스트는 BeanDefinition으로 만들어진 메타정보를 담은 오브젝트를 사용해 IoC와 DI 작업을 수행.
https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/BeanDefinition.html


3. WebApplicationContext
https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/context/WebApplicationContext.html
웹 환경에서 사용할 때 필요한 기능이 추가된 애플리케이션 컨텍스트

Like generic application contexts, web application contexts are hierarchical. There is a single root context per application, while each servlet in the application (including a dispatcher servlet in the MVC framework) has its own child context.

In addition to standard application context lifecycle capabilities, WebApplicationContext implementations need to detect ServletContextAware beans and invoke the setServletContext method accordingly.


웹 환경에선느 main() 메소드 대신 서블릿 컨테이너가 브라우저로부터 오는 HTTP 요청을 받아서 해당 요청에 매핑되어 있는 서블릿을 실행해주는 방식으로 동작. 서블릿이 일종의 main()메소드와 같은 역할.


스프링은 이런 웹 환경에서 애플리케이션 컨텍스트를 생성하고 설정 메타 정보로 초기화해주고, 클라이언트로부터 들어오는 요청마다 적절한 빈을 찾아서 이를 실행해주는 기능을 가진 DispatcherServlet이라는 이름의 서블릿을 제공.


* 자바 코드에 의한 빈 등록: @Configuration클래스의 @Bean 메소드
하나의 클래스 안에 여러개의 빈을 정의 할 수 있다. 또 애노테이션을 이용해 빈 오브젝트의 메타정보를 추가하는 일도 가능.


* 프로퍼티 값 설정
1. XML : <property> 와 전용 태그
```
<bean id="hello" ...>
    <property name="name" value="Everyone" />
    ...
</bean>
```

2. @Value
빈이 사용해야 할 단순한 값이나 오브젝트를 코드에 담지 않고 설정을 통해 런타임시에 주입해야하는 이유는?

  1. 환경에 따라 매번 달라질 수 있는 값
    대표적으로 DataSource 타입의 빈에 제공하는 DriverClass, URL, UserName, Password
    또는 파일 경로처럼 환경에 의존적인 정보이거나 작업에 대한 타임아웃처럼 상황에 따라 달라질 수 있는 값을 소스코드의 수정없이 지정해주기 위해서.

  2. 초기값을 미리갖고 있찌않음.
    테스트나 특별한 이벤트 때는 초기값 대신 다른 값을 지정
```
@Value("${database.username}")
String username;
```
이때는 database.username 속성이 정의된 database.properties 파일을 XML에 지정해둬야 함.

```
<context:property-placeholder location="classpath:database.propertiel"/>
```
  1. 기본타입
  ```
  boolean flag;
  public void setFlag(boolean flag) {this.flag=flag;}

  in XML
  <property name="flag" value="true" />
  ```

  2. 배열
  @Value("1,2,3,4") int[] intarr;


https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config


