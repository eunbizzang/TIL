https://spring.io/guides/gs/gateway/

circuitbreak란

- api가 route 하는 과정에서 해당 api의 응답이 느려져서(timeout) , 에러가 나는(exception) 중에 계속해서 해당 api 를 불러서 여러 가지 문제를 확산(해당 api 가 DB connection을 점유, 또는 서버 리소스를 잠식 한다 등) 시키는 문제를 방지 하고자 . api gateway에서 특정 조건이 (호출수 대비 실패율) 만족되면 gateway에 api를 호출하지 않고 error 처리를 하는것을 말한다.



https://www.baeldung.com/spring-cloud-circuit-breaker