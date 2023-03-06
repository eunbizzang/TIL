https://riverblue.tistory.com/m/46


XSS를 막기위한 XSS Filter

1. 요청에서 데이터를 가져온다.

2. XSS를 escape한 문자로 replace해서 다시 넣어준다.

 
lucy필터는 한계가있다. multipart/form 과 json같은 request body 데이터는 필터링이 안된다. 

때문에 아래 3개의 기능 개발이 필요.

1. lucy처럼 일반 폼데이터 필터링

2. json데이터 필터링 

3. multipart/form데이터 필터링