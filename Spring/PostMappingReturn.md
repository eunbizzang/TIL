https://threeyears.tistory.com/98
https://stackoverflow.com/questions/12837907/what-to-return-if-spring-mvc-controller-method-doesnt-return-value


return void 하면 호출한 url의 경로로 뷰를 찾음.



You can simply return a ResponseEntity with the appropriate header:
```
@RequestMapping(value = "/updateSomeData" method = RequestMethod.POST)
public ResponseEntity updateDataThatDoesntRequireClientToBeNotified(...){
....
return new ResponseEntity(HttpStatus.OK)
}
```