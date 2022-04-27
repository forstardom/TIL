# 플러시(Flush)

## **플러시(Flush) 란?**

```
영속성 컨텍스트의 변경 내용을 DB에 반영하는 것
```

- 영속성 컨텍스트를 비우지 않음
- 영속성 컨텍스트의 변경 내용을 DB에 동기화
- 트랜잭션이라는 작업 단위가 중요 -> commit 직전에만 동기화하면 됨

## **플러시가 발생하면?**

- 변경 감지
- 수정된 엔티티 쓰기 지연 SQL 저장소에 등록
- 쓰기 지연 SQL 저장소의 쿼리를 DB에 전송(등록, 수정, 삭제 쿼리)

## **영속성 컨텍스트를 플러시하는 방법**

- em.flush() - 직접 호출
- Transaction commit = 플러시 자동 호출
- JPQL 쿼리 실행 - 플러시 자동 호출

## **플러시 모드 옵션**

```
em.setFlushMode(FlushModeType.COMMIT)
```

- FlushModeType.AUTO  
  커밋이나 쿼리를 실행할 때 플러시(default)

- FlushModeType.COMMIT  
  커밋할 때만 플러시
