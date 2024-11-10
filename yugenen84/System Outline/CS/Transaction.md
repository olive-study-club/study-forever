### Tranction 개념
- 데이터베이스에서 하나의 그룹으로 처리되어야 하는 명령문들을 모아 놓은 논리적인 작업 단위
- 정상일 경우 Commit 되어 종료되고 처리에 실패하면 Rollback 된다

### Tranction  4가지 특징_ACID
- ACID를 통해 데이터의 안정성과 무결성을 보장함
- Atomicity (원자성)
    - 트랜젝션의 작업이 부분적으로 실행되거나 중단되지 않는 것을 보장한다
    - 해당 작업이 모두 DB 에 반영되거나 아예 반영되지 않아야 한다(All or Nothing)

- Consistency (일관성)
    - 작업처리 결과는 항상 일관성을 유지하여야 한다
    - 처리 전과 후의 고정 요소가 동일해야 한다
    - 처리 전과 후의 데이터 모델의 모든 제약 조건 및 타입이 동일해야 한다
    - 트리거를 통해 보장해야 한다
            - 트리거는 특정 테이블에 INSERT, DELETE, UPDATE 같은 DML 문이 수행되었을 때, 데이터베이스에서 자동으로 동작하도록 작성된 프로그램
            - 사용자가 직접 호출하는 형태가 아니라, 데이터베이스에서 자동적으로 호출하는 것이 특징
            - 따라서 트리거를 통해서 데이터베이스의 일관성이 보장될 수 있는데, 예를 들어 한쪽 데이터베이스의 테이블에 정보의 수정이 일어났을 경우 다른 쪽 테이블에도 함께 정보가 수정될 수 있도록 명시적으로 자동 업데이트를 하는 명령 등을 구성하게 됩니다.

-  Isolation (독립성 || 고립성 || 격리성)
    - 여러 개의 트랜젝션을 작업할 때 어떤 트랜젝션도 다른 트랜젝션이 작업에 끼어들 수 없다

- Durability (영속성 || 지속성)
    - 트랜젝션이 성공적으로 처리되면 결과는 영구적으로 반영

### Transaction 의 연산
- Commit 연산
    - 트랜젝션이 성공적으로 처리된 경우 수행. 최종결과를 DB에 반영

- Rollback 연산
    - 트랜젝션의 처리가 실패되는 경우 작업을 취소하는 연산이며 DB를 트랜젝션 수행전과 일관된 상태로 되돌린다

- Active 연산
    - 트랜젝션이 실행 중인 상태

- Partially Committed
    - 트랜젝션의 ```Commit``` 명령이 도착한 상태
    - ```Commit``` 이전까지의 SQL 쿼리가 수행되고 Commit만 남은 상태

- Failed
    - 트랜젝션 실패 상태

- Committed
    - 트랜젝션 완료 상태

- Aborted
    - 트랜젝션 취소 상태


- Source 
    - *https://velog.io/@jsplix__/DataBase-Transaction-%EC%9D%B4%EB%9E%80*
    - *https://wonit.tistory.com/462*
    - *https://jaehoney.tistory.com/232*
    - *https://velog.io/@shasha/Database-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%A0%95%EB%A6%AC*
