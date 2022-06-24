https://www.inflearn.com/questions/30076

https://oingdaddy.tistory.com/350


https://jojoldu.tistory.com/251


* Entity 를 그대로 return 할 경우
1. Entity 변화 시, API도 변경
API 통신에서 Entity를 그대로 return 하는 경우 DB가 변경되면 API도 변경되어야 함.
API가 변경되려면 관련된 모든 사람들이 코드를 수정해야하는 상황이 발생.

2. 트래픽 증가
Entity를 그대로 return 할 경우 불필요한 정보로 인해 트래픽이 증가할 수 있음.

--> View Layer와 DB Layer를 철저하게 역할 분리

* Entity 클래스 
Entity의 필드 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가하셔야만 합니다.

예를들어 주문 취소 메소드

```
잘못된 사용
public class Order{
    public void setStatus(boolean status){
        this.status = status
    }
}

public void 주문서비스의_취소메소드 (){
   order.setStatus(false);
}

올바른 사용
public class Order{
    public void cancelOrder(){
        this.status = false;
    }
}
public void 주문서비스의_취소메소드 (){
   order.cancelOrder();
}
```


Service단을 중심으로 DB ↔ Service는 엔티티, Service → Controller는 DTO를 사용


의존관계를 생각해야한다.(의존관계가 복잡해지면 잘못된 코드)

방법


1. ModelMapper
    
    
    타이트하게 ModelMapper의 config를 구성하기(ex.필드명이 변경되었을때의 버그)
    

    1. 매칭 전략을 어떻게 할 것인가


    Strict, Loose, Standard 중 필요하다면 Strict로 강제 해야 합니다.
    Standard는 토큰으로 전략적 매칭하기 때문에 원치 않는 매핑이 발생할 수 있습니다.
    

    2. 예외 필드 관리


    필드 명이 다르지만 매핑이 되어야 하는 경우 -> map()
    매핑이 필요 없는 필드는 스킵 -> skip()


    3. validation


    매핑이 끝난 후 ModelMapper#validate 메서드로 skip된 필드 이외의 모든 필드가 매핑되었는지 확인합니다.
    이때 value가 null인 것과 상관없이 mapped가 되었는지 확인합니다.
    본문에 작성한 것처럼 Exception을 throw 하기 때문에 이 지점이 병목이 될 수 있으므로 주의가 필요합니다.
    http://modelmapper.org/user-manual/configuration/#matching-strategies

2. 한땀한땀


3. JPQL 에서 DTO로 바로 변환


* Page<ObjectEntity> to Page<ObjectDTO>
https://stackoverflow.com/questions/39036771/how-to-map-pageobjectentity-to-pageobjectdto-in-spring-data-rest
