dirtyChecking

더티체킹은 Transaction 안에서 엔티티의 변경이 일어나면, 변경 내용을 자동으로 데이터베이스에 반영하는 JPA 특징

데이터베이스에 변경 데이터를 저장하는 시점

1. Transaction Commit
2. EntityManager Flush
3. JPQL 사용

JPA에서는 트랜잭션이 끝나는 시점에 변화가 있는 모든 엔티티 객체를 데이터베이스에 자동으로 반영해준다.
변화의 기준은 최초 조회 상태

```
@Transactional

void updateMember(Member memberParam)
Member findMember = em.find(Member.class, memberParam.getId());

findMember.setName(memberParam.getName());
```
entityManager로 entity를 직접 꺼내, 값을 수정


@Transactional(readOnly = false)
   	public void updateItem(Long itemId, Item item) { // item : 파리미터로 넘어온 준영속 상태의 엔티티 
        
    	// itemId, name, price, stockQuantity : 수정할 값
    
        // 영속성 컨텍스트에서 엔티티를 다시 조회한다.
        Item findItem = itemRepository.findOne(itemId);
        
        // 데이터를 수정한다.
        findItem.setName(item.getName());
        findItem.setPrice(item.getPrice());
        findItem.setStockQuantity(item.getStockQuantity()); 
    }
@Transactional으로 인하여 로직이 끝날 때 JPA에서 트랜잭션 commit 시점에 변경 감지(Dirty Checking)한 후 Flush를 하게 되기 때문에 따로 itemRepository.save() 할 필요가 없다.

```
@Transactional  
public void cancelOrder(Long orderId) {  
    //주문 엔티티 조회  
    Order order = orderRepository.findOne(orderId);  

    //주문 취소  
    order.cancel();  
}
```

---
merge 사용
```
@PostMapping("/members/{memberId}/editName")
public String updateMemberName(@ModelAttribute("form") MemberNameEditForm form){
Member member = new Member();

member.setId(form.getId());
member.setName(form.getName());

em.merge(member);

return "redirect:/members";
```
merge가 호출되면 우선 해당 엔티티를 1차 캐시에서 먼저 조회하고, 

없다면 식별자로 DB에서 엔티티를 검색해 가져와 준영속 상태의 엔티티 값을 대입

save
```
public void save(Member member){

  if(Member.getId() == null){
     em.persist(member);
  } 
  
  else{ 
     em.merge(member);
  }
}
```
위와 같이 Id가 없으면 새로 생성(persist), 있으면 병합(merge)을 호출

https://velog.io/@jiny/JPA-%EB%8D%94%ED%8B%B0-%EC%B2%B4%ED%82%B9Dirty-Checking-%EC%9D%B4%EB%9E%80

https://brunch.co.kr/@purpledev/32

Bulk Update를 실행하는 경우 영속성 컨텍스트의 관리를 받지 못하게 되므로 업데이트 연산 이후 엔티티를 가지고 후 처리가 필요한 경우에는 엔티티를 다시 조회해야한다.