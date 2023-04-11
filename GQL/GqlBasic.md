https://tech.kakao.com/2019/08/01/graphql-basic/

로직은 비지니스 로직 레이어 (다른 파일의 다른 함수)에 작성을 하는 것을 권장합니다. 위 그림에도 나왔지만 이는 REST API를 제작할때 사용하는 패턴과 동일한 패턴입니다.
```
    requestPaymentSession: async (parent, { 
      pgId, name, sex, birthDay, phoneNumber, amount, productName, ref 
    }, context, info) => {
      const ret = await requestPaymentSession({ pgId, name, birthDay, phoneNumber, sex, amount, productName, ref })

      return removeSymbol(ret)
    },
    requestPaymentApprove: async (parent, {
      sessionKey, authNumber
    }, context, info) => {
      const ret = await requestApprovePayment({ sessionKey, authNumber })

      return removeSymbol(ret)
    }
```