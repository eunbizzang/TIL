https://velog.io/@tjeong/Spring-Message-%EC%82%AC%EC%9A%A9%EB%B2%95

message.properties
```
// {messageCode}={messageContent}
range.distance="Too Far"
```

(1) Spring
```
  @Bean
  public MessageSource messageSource() {
      ResourceBundleMessageSource MS = new ResourceBundleMessageSource();
      // MesageSource의 인코딩 방식 설정
      MS.setDefaultEncoding("utf-8");
      // 메시지를 관리할 파일 이름 지정
      // messages라고 지정하면 src/main/resources/messages.properties 로 설정
      MS.setBasenames("messages");
      return MS;
}
```

(2) SpringBoot
SpringBoot에서는 ResourceBundleMessageSource가 이미 bean으로 등록되어 있기 때문에 Message를 관리할 파일의 경로만 application.properties에서 경로 설정만 해주면 됩니다.

```
# INTERNATIONALIZATION (MessageSourceAutoConfiguration)
spring.messages.always-use-message-format=false # Set whether to always apply the MessageFormat rules, parsing even messages without arguments.
spring.messages.basename=messages # Comma-separated list of basenames, each following the ResourceBundle convention.
spring.messages.cache-seconds=-1 # Loaded resource bundle files cache expiration, in seconds. When set to -1, bundles are cached forever.
spring.messages.encoding=UTF-8 # Message bundles encoding.
spring.messages.fallback-to-system-locale=true # Set whether to fall back to the system Locale if no files for a specific
```
