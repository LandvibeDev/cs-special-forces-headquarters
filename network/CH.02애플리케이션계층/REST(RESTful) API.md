## REST(RESTful) API

### REST API의 탄생
* HTTP 설계의 우수성에 비해 제대로 사용되어지지 못하여 웹의 장점을 최대한 활용할 수 있는 아키텍처로써 REST를 발표했다고 함.

### REST가 필요한 이유
* 애플리케이션 분리 및 통합
* 다양한 클라이언트의 등장
* 최근의 서버 프로그램은 다양한 브라우저와 안드로이드, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 함.
* 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 됨.

### REST 구성
* 자원(Resource) : URI
	* 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재함.
	* 자원을 구별하는 ID는 '/groups/:group_id'와 같은 HTTP URI다.
	* Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청함. 
* 행위(Verb) : HTTP Method
	* HTTP 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공함. 
* 표현(Representations)
	* Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이제 적절한 응답(Representation)을 보냄.
	* REST에서 하나의 자원은 JSON, XML, TEXT, RSS등 여러 형태의 Representation으로 나타낼 수 있음.
	* JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적. 

### REST의 특징
* Uniform Interface(유니폼 인터페이스)
	* Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말함.
	* HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능 (특정 언어나 기술에 종속되지 않음)
* Stateless(무상태성)
	* REST는 무상태성 성격을 가지고 있습니다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다.
	* 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 됨.
	* 따라서 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않아 구현이 단순해짐.
	* 고급진 표현
		* Client의 context를 Server에 저장하지 않음
		* Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리함.
			* 각 API 서버는 Client의 요청만을 단순 처리함.
			* 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안됨.
			* 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용.
			* Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아짐. 
* Cacheable(캐시 가능)
	* REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에 웹에서 사용하는 인프라를 그대로 활용 가능.
	* 따라서 HTTP가 가진 캐싱 기능이 적용 가능.
	* 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있음.
	* HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-tag를 이용하면 캐싱 구현이 가능.	
	* last-modified: http 헤더에 서버가 알고있는 가장 마지막 수정된 날짜와 시각을 담고 있음.
	* E-tag: 특정 버전의 리소스를 식별하는 식별자. ex) 특정 URL의 리소스가 변경되면, 새로운 E-tag가 생성됨. 지문같은 역할을 하면서 다른 서버들이 추적하는 용도에 이용되기도 함.
* Self-descriptiveness(자체 표현 구조)
	* REST API 메시지만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구조로 되어 있음.
* Client-Server 구조
	* 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 됨.
	* REST 서버는 API 제공하고 비즈니스 로직 처리 및 저장을 책임짐.
	* 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하고 책임짐.
	* 각각의 역할이 구분됨. 따라서 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됨.
* 계층형 구조
	* Client는 REST API Server만 호출함.
	* REST Server는 다중 계층으로 구성될 수 있음.
		* API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있음.
		* 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있음. 
	* proxy, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 함.

### REST API 디자인 가이드
* URI(Uniform Resource Identifier), URL(Uniform Resource Locator)
* URI은 정보의 자원을 표현해야 함.  
* 자원에 대한 행위는 HTTP method(GET,POST,PUT,DELETE)로 표현함.
	* HTTP method를 이용해서 CRUD를 할 수 있음 

#### REST API 중심 규칙
* 참고 리소스 원형
	* 도큐먼트: 객체 인스턴스나 데이터베이스 레코드와 유사한 개념
	* 컬렉션: 서버에서 관리하는 디렉터리라는 리소스
	* 스토어: 클라이언트에서 관리하는 저장소 
* URI은 정보의 자원을 표현해야 한다.
	* resource는 동사보다는 명사를 사용.
	* resource의 도큐먼트 이름으로는 단수 명사를 사용해야 함.
	* resource의 컬렉션 이름으로는 복수 명사를 사용해야 함.
	* resource의 스토어 이름으로는 복수명사를 사용해야 함.
* 자원에 대한 행위는 HTTP method(GET,POST,PUT,DELETE)로 표현.
	* URI에 HTTP Method가 들어가면 안됨.
	* URI에 행위에 대한 동사 표현이 들어가면 안됨.(CRUD 기능을 나타내는 것은 URI에 사용하지 않음) 
* 슬래시 구분자(/)는 계층 관계를 나타내는데 사용.
* URI의 막지막 문자로 /를 포함하지 않음.
* -은 URI 가독성을 높이는데 사용.
* _은 URI에 사용하지 않음. 
* URI경로에는 소문자를 사용.
* 파일 확장자는 URI에 포함시키지 않음.
* 리소스 간의 관계를 표현할 수 있음.
	* ex) GET: /users/{userid}/devices (일반적으로 소유 'has'의 관계를 표현할 때) 

### REST API
* REST 기반으로 서비스 API를 구현한 것

## RESTful의 개념

### RESTful이란
* RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어
	* REST API를 제공하는 웹 서비스를 RESTful하다고 할 수 있음
* RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것은 아님
	* 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭 됨.

### RESTful의 목적
* 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
* RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이므로 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요 없음.

### RESTful 하지 못한 경우
* CRUD 기능을 모두 POST로만 처리하는 API
* route에 resource, id 외의 정보가 들어가는 경우 (/students/updateName)