https://www.itworld.co.kr/news/252478

JSON 파싱 및 생성
JSON을 파싱하고 생성한다는 것은 각각 JSON 읽기와 만들기를 의미한다. JSON.stringify()의 예시는 이미 살펴본 것처럼 메모리 내 객체 표현을 취해 JSON 문자열로 변환하기 위한 자바스크립트 프로그램의 내장 메커니즘이다. 반대로, 즉 JSON 문자열을 받아 메모리 내 객체로 변환하려면 JSON.parse()를 사용한다.


다른 대부분의 언어에서는 파싱과 생성을 위해 서드파티 라이브러리를 사용해야 한다. 예를 들어 자바에는 수많은 라이브러리가 있지만 가장 많이 사용되는 라이브러리는 잭슨(Jackson)과 GSON이다. 이 두 라이브러리는 자바스크립트의 stringify 및 parse보다 더 복잡하지만 맞춤 형식과의 매핑, 다른 데이터 형식 처리와 같은 고급 기능을 제공한다. 자바스크립트에서는 JSON을 서버로 보내고 받는 것이 일반적이다. 예를 들어 내장된 fetch() API를 사용한다. 이 경우 <예시 7>과 같이 응답을 자동으로 파싱할 수 있다.

<예시 7> fetch()로 JSON 응답 파싱하기
```
fetch('https://the-one-api.dev/v2/character')
  .then((response) => response.json())
  .then((data) => console.log(data));
```