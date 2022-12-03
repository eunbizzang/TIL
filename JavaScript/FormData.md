https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-FormData-%EC%A0%95%EB%A6%AC-fetch-api


```
let formData1 = new FormData($("#form Id")); // 제이쿼리인 경우
let formData2 = new FormData(document.getElementById("form Id"));
```


자바스크립트에서 서버로 form data를 보내려면 body 속성 부분을 일반적인 json이나 객체 타입 형태가 아닌 form data 타입 형식에 맞춰서 보내야 한다
