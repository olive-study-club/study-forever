## API 와 전문통신방식(Fixed Length Format)

### 전문통신방식

 #### 개념
 - 통신에 참여하는 애플리케이션들이 주고 받을 데이터의 포맷을 서로 약속하고 데이터 패킷을 전송하고 수신하는 방식
 - 클라이언트는 약속된 데이터 패킷의 포맷에 맞춰 패킷을 생성, 서버로 전송하고
 서버는 패킷을 읽어 들이고 패킷에 기록된 데이터를 해석해 *** "작업수행- 결과" *** 를 패킷에 기록해 클라이언트에게 반환
 - 시스템 간의 통신에서 데이터 송수신 format을 정하는 것도 중요하며 송수신 전문의 형태는 JSON, XML, Fixed Length 로 구성이 가능함

#### 특징
 - 바이트 배열 형태로 전문을 구성하는 데이터 타입은 char로 구성하는 것이 좋음
     - int, long 등 이종간 시스템에서 encoding 오류 발생가능
 - 정해진 바이트 배열 구조로 상대에게 전송하면 상대방도 정해진 규칙에 따른 바이트 배열로 응답
 - 하드웨어와 밀접한 서비스와 데이터를 주고 받을 때 사용함

#### 구조
 - 헤더 : 공통 데이터 / 바디 : 실제 통신에 필요한 데이터 
 - 예비 영역 : 통신 중 추가로 생긴 규칙으로 인해 추가 데이터를 보내야할 경우 구조를 다시 설계하지 않기 위한 용도 

---

### API 

#### 개념
- 애플리케이션 소프트웨어를 구축하고 통합하기 위한 정의 및 프로토콜로, 애플리케이션 프로그래밍 인터페이스를 나타냄
- 접근 권한이 있는 상대방이 API를 통해 서버에서 제공하는 데이터를 요청해서 사용가능함
- DB서버에 관련 정보를 보관하고 다른 응용 프로그램이 DB서버에서 필요로 하는 데이터를 조회하고 사용할 수 있도록 API를 개발함

#### HTTP API
- HTTP 를 사용하여 프로그램끼리 소통하는 API를 말하며 OPEN API, kakao API 등 대부분 API는 HTTP라는 통신 규칙으로 소통함

#### REST API(Representational State Transfer)
- 네트워크 자원을 정의하고 처리하는 방법 전반을 일컫는 네트워크 아키텍처 스타일로 HTTP를 활용하기 위한 원칙
- URI로 자원을 표현하고 자원의 상태(행위)에 대한 정의는 HTTP Method로 하는 것이 REST API를 설계하는 중심 규칙임
   - 중심규칙
       - URI로 리소스를 표현
       - 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현
       - 잘못된 예시: 행위(delete) 표현 불가
       ```
       GET / members/delete/1
       ```
       - 정상적인 예시
       ```
       DELETE /members/1
       ```
       - 정보를 가져오는(조회) 행위는 GET
       ```
       GET /members/1
       ```

       - 정보를 생성 하는 행위 POST 
       ```
       POST /members/2
       ```

   - 자원의 표현 방식
       - document, collection, store, controller 의 4가지 방식
       - 자원은 URI로 표현되며 동사는 사용하지 않음

       - document 
           - 1개의 객체를 나타내는 것으로 DB의 record와 유사한 개념임. REST에서는 리소스 집합(collection) 중 하나로 표현되며 일반적으로 단수명사로 collection 뒤에 "/" 를 통해 구분
       - collection
           - Resource들의 집합으로 클라이언트들은 일반적으로 새로운 리소스를 추가하거나 단일 리소스가 아닌 다량의 리소스가 필요할 때 collection을 호출. 복수명사 사용
       - http://restapi.example.com/sports/soccer
           - sports라는 컬렉션과 soccer라는 도큐먼트로 표현

           --- 
           - 참조 
           - https://itstart-190126.tistory.com/entry/API%EC%99%80-%EC%A0%84%EB%AC%B8%ED%86%B5%EC%8B%A0%EC%9D%B4%EB%9E%80-%EA%B0%9C%EB%85%90-%EC%95%8C%EC%95%84%EB%91%90%EA%B8%B0
           - https://hoyeonkim795.github.io/posts/rest_api/
           - https://bentist.tistory.com/37

