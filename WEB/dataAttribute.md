https://velog.io/@yunsungyang-omc/HTML-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%86%8D%EC%84%B1-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-data-attribute



데이터 속성의 장점은 이전과 같이 hidden으로 태그를 숨여두고 데이터를 저장할 필요가 없다는 점이다. 따라서 훨씬 HTMl 스크립트가 훨씬 간결해진다. 또한 하나의 HTMl 요소에는 여러 데이터 속성을 동시에 사용할 수도 있다.


```
<input type="text" data-value="001"  data-code="c03"  id="username">     
```

자바스크립트에서 데이터 속성을 조작하기 위한 방법은 여러가지가 있지만, 기본적으로 DOM객체를 통해 데이터 속성 조작이 가능하다.

```
<input type="text" data-value="001"  data-code="c03"  id="username">   
var input = document.querySelector('#username');
console.log(input.dataset);
```

특정 속성값만 추출하기
```
console.log(input.dataset.code);
console.log(input.dataset['code']);
```

데이터 속성 값 바꾸기
```
let input = document.querySelector('#username');
input.dataset.code = 'aaa'
```