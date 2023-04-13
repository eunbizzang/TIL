https://developer.mozilla.org/ko/docs/Web/API/Element/classList


classList 사용은 공백으로 구분된 문자열인 element.className을 통해 엘리먼트의 클래스 목록에 접근하는 방식을 대체하는 간편한 방법
```
const elementClasses = elementNodeReference.classList;
```


메서드

```
add( String [, String [, ...]] )
```
지정한 클래스 값을 추가한다. 만약 추가하려는 클래스가 엘리먼트의 class 속성에 이미 존재한다면 무시한다.


```
remove( String [, String [, ...]] )
```
지정한 클래스 값을 제거한다.