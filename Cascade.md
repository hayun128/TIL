# Cascade


<aside>
✨ 객체의 연관관계에 옵션으로 줄수 있는 값

</aside>

**엔티티의 상태 변화를 전파**시키는 옵션

엔티티의 상태 변화가 잇으면 연관(ex.ManyToOne)된 엔티티에도 상태변화를 전이 시킨다

# 엔티티의 상태

1. Transient
    
    DB와 매핑된 것이 없음
    

1. persistent
    
    저장을 하면 JPA가 아는(관리하는) 상태
    
    - .save()를 했어도 바로 DB에 객체 데이터가 들어가는 것은 아님
        
        JPA가 persistent로 관리하고 있다가 후에 데이터를 저장한다 
        

1. Detached
    
    JPA가 더는 관리하지 않음
    
    - 다시 JPA가 제공하는 기능흘 사용하려면 persistent로 돌아가야함

1. Removed
    
    JPA가 관리하지만 commit이 일어나면 삭제된다
    

예를 들어 보드가 있고 그 보드에 달린 댓글은 보드가 저장되면 같이 저장되고 보드가 삭제되면 같이 삭제 된다고 할때 사용할수 있다 

# 속성

CascadeType

```java
@ManyToOne(cascade = CascadeType.MERGE)
```

.All

모든 cascade를 적용

.PERSIST

엔티티를 영속화할때 연관된 엔티티도 함께 유지

.MERGE

엔티티 상태를 병합할때 연관된 엔티티도 모두 병합

.REMOVE

엔티티를 제거할때 연관된 엔티티도 모두제거

.DETACH

부모 엔티티를 detach()하면 연관된 엔티티도 detach() 상태 ⇒ 변경사함 반영X

.REFRESH

상위 엔티티를 새로고침(Refresh) 할때 연관된 엔티티도 모두 새로고침
