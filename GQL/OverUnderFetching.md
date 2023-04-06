https://hanamon.kr/graphql%EC%9D%B4%EB%9E%80-api%EB%A5%BC-%EC%9C%84%ED%95%9C-%EC%BF%BC%EB%A6%AC-%EC%96%B8%EC%96%B4/

# Over-Fetching
예를 들어, 사용자의 데이터를 조회하는 /user/API가 있다고 가정한다.

이 때, 사용자 번호: 1 에 해당하는 데이터를 조회한다면 아래와 같은 형태가 된다.


```
GET /user/1/
response body
{
"user_no":1,
"user_name": "test",
"user_grade": "VVIP",
"zip": "11053",
"last_login_timetamp": "2019-08-08 12:11:44",
...
}
```
여기에서 클라이언트는 1번에 해당하는 유저의 이름만을 사용하고자 한다고 해도 유저 이름만 반환하는 API가 없다면 위와 같은 /user/1/API를 호출한 다음, user_name을 가져와 사용해야한다. 이 때, user_grade, zip 등등의 데이터는 사용하지 않는 데이터도 같이 반환받는다. 이는 곧 리소스의 낭비라고 볼 수 있고 이와 같은 낭비를 Over-Fetching이라 명한다.

# Under-Fetching
쇼핑몰 서비스의 경우, 로그인한 사용자의 장바구니 정보를 보여준다고 가정하면 여러 API를 호출하게 된다.

```
/user/1/
/cart/
/notification/
/wish/
...
```

요청에 맞게 유효한 데이터를 보여주기 위해 여러 API를 호출하게 되는 경우를 Under-Fetching이라 한다.



GraphQL은 위에서 설명한 것처럼 REST API의 한계를 극복하고자 나왔다.

Endpoint는 통상 1개만 생성하고 클라이언트에게 필요한 데이터는 클라이언트가 직접 쿼리를 작성, 호출하여 반환 받는다.

위의 Under-Fetching 문제를 GraphQL을 사용하면 손쉽게 해결된다.

요청 쿼리
```
query{
      user(user_no:1){
            user_name  
      }
}
```
반환 데이터
```
{
      "data": {
            "user": {
                  "user_name": "jim",
            }
      }
}
```


