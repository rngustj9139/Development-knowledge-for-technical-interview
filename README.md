# Development-knowledge-for-technical-interview
기술면접을 위한 개발지식 정리

> created by 경희대학교 소프트웨어융합학과 구현서 [mnb9139@khu.ac.kr]

---------------------------

## 기술파트(서버 - 스프링)

* ### REST API란?
  자원을 URI로 표현하고, 자원에 대한 행위를 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다. 주로 HTTP 요청, 응답 메세지 바디에 데이터를 넣고 송수신한다.

* ### HTTP의 특징
  1.비연결성 - 클라이언트와 서버가 한 번 연결을 맺은 후, 클라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어버리는 성질입니다.(만약 서버에서 다수의 클라이언트와 연결을 계속 유지해야 한다면, 이에 따른 많은 리소스가 발생하게 됩니다. 따라서 연결을 유지하기 위한 리소스를 줄이면 더 많은 연결을 할 수 있으므로 비연결적인 특징을 갖습니다)
  
  2.무상태프로토콜 - 비연결성으로 인해 서버는 클라이언트의 상태를 기억할 수 없는데, 이를 Stateless라고 합니다. (매번 새로운 인증을 해야하는 번거로움 발생 => 상태를 기억하기 위해 쿠키를 사용해야함)

* ### TCP/IP란? TCP와 UDP의 차이점은?
  인터넷에서 컴퓨터들은 pc의 주소(IP)를 통해 통신합니다. (지정한 ip주소에 패킷이라는 통신 단위로 데이터 전달, 패킷이 목적지에 도착한 후 응답패킷이 되돌아옴)
  
  IP는 비연결성(패킷을 받을 대상이 없거나 통신 불능 상태여도 패킷 전송), 비신뢰성(패킷이 중간에 사라짐, 패킷이 순서대로 오지 않음)이라는 한계가 존재합니다.
  
  TCP/IP는 위의 한계를 극복할 수 있게 합니다.(패킷에 순서정보, 검증정보, 전송제어정보 까지 포함)
  
  TCP는 연결지향(3 way handshake)라서 무조건 연결을 한뒤 데이터를 송수신하며 데이터 전달 보증, 순서 보장을 합니다. => 신뢰할 수 있는 프로토콜
  
  UDP는 연결지향이 아니지만 TCP보다는 속도가 빠르다는 장점이 존재합니다.
  
* ### HTTP METHOD
  1.GET - 서버에게 리소스를 달라는 요청 (조회)
  
  2.POST - 서버에게 리소스를 보내면서 생성해 달라고 요청 (메세지 바디를 통해 서버로 요청 데이터 전달)
  
  3.DELETE - 서버에게 리소스의 삭제를 요청
  
  4.PUT - 리소스 업데이트(없으면 새로 생성 or 존재하면 덮어쓰기, 요청시 데이터를 일부분만 보낸경우 나머지 필드는 삭제됨)
  
  5.PATCH - 리소스 업데이트(일부분만 수정 가능)

* ### 동기, 비동기, 블로킹, 논블로킹이란?
  1.동기 - 하나의 작업이 끝나야지 이후 다른 작업을 수행 가능(혹은 동시에 같이 시작하고 동시에 같이 끝남)
  
  2.비동기 - 하나의 작업이 수행중이여도 다른 작업 수행가능
  
  3.블로킹 - 하나의 작업이 수행 중이었다가 멈추고 도중에 다른 작업이 수행되면서 다른 작업의 결과물을 받아서 다시 작업을 재개하는 방식
  
  4.논블로킹 - 하나의 작업이 수행 중에 다른 주체에게 작업을 요청하고 그 결과를 받을때까지 기다리지 않으면서 자신의 작업을 계속 수행하는 방식
  

* ### 컴포넌트 스캔이란?
  @Controller, @Service, @Repository같은 어노테이션을 이용해 클래스를 스프링 컨테이너에 스프링 빈으로 등록 하는 것을 의미합니다. (빈 설정 정보 파일이 없어도 자동으로 등록, @Autowired 어노테이션을 사용하면 의존관계 자동 주입 가능)

* ### RDB란?
  RDB는 관계형 데이터 베이스이며 모든 데이터를 2차원 테이블 형태로 표시합니다. 또한 각각의 테이블들은 상호관련성(relation - 관계)을 가집니다. (외래키를 이용해 관계를 맺은 다른 테이블을 조인할 수 있습니다.)
  
* ### 쿠키, 캐시, 세션의 차이
  1.쿠키 - 클라이언트가 처음 서버에서 받은 쿠키를 쿠키저장소에 저장하고 매번 요청을 할 때마다 쿠키저장소에서 쿠키를 꺼내 같이 서버로 전송합니다. (ex - 로그인 유지)
  
  2.캐시 - 서버에서 받는 파일들(ex - 이미지 파일들)을 매번 네트워크를 통해 받는 것은 비효율적입니다. 따라서 처음 접속할때 받은 이미지 파일을 브라우저 캐시에 저장해놓고 클라이언트는 그 캐시를 계속 사용합니다. 
  
  3.세션 - 예측가능한 쿠키 값은 임의로 변경이 될 수 있습니다. 또 쿠키에 저장된 중요 정보는 탈취될 가능성도 존재하며 이는 보안 문제를 야기합니다. 따라서 중요한 정보는 서버쪽에서 모두 저장되어야합니다. 이로인해 서버쪽에서 세션저장소를 만들고 예측 불가능한 토큰을 쿠키로 사용해야합니다.  

* ### MVC 패턴이란?
  MVC 패턴이란 애플리케이션의 구성요소를 Model, View, Controller로 분리하는 것을 의미합니다. 컨트롤러는 요청을 받거나, 모델에 데이터를 담아서 뷰(사용자에게 보여지는 영역)에 전달합니다.
 또 컨트롤러는 서비스계층을 주입받아서 비즈니스 로직이 수행되도록하고 서비스계층은 DAO를 주입받아 DB에 접근할 수 있습니다.

* ### 싱글톤 패턴이란?
  싱글톤(Singleton) 패턴은 스프링 컨테이너에서 객체의 인스턴스를 오직 1개씩만 생성하는 것을 의미합니다. 싱글톤 패턴의 장점은 아무래도 메모리 측면입니다. 최초 한번의 new 연산자를 통  해서 고정된 메모리 영역을 사용하기 때문에 메모리 낭비를 방지할 수 있습니다. 뿐만 아니라 이미 생성된 인스턴스를 반환하니 속도 측면에서도 이점이 있습니다.
  
* ### 프로토타입 패턴이란?
  싱글톤 패턴과는 달리 스프링 컨테이너가 매번 새로운 인스턴스를 생성해서 반환합니다.

* ### 스레드와 프로세스의 차이란?, 동시성과 병렬성이란?
  프로그램이 실행되서 돌아가고 있는 상태, 즉 컴퓨터가 어떤 일을 하고있는 상태를 프로세스라고 합니다. 동시성은 프로세서(cpu)가 하나의 프로세스를 처리하다가 도중에 다른 프로세스를 처   리하는등 여러 프로세스를 돌아가면서(context switching) 일부분씩 진행하는 것을 의미합니다. 병렬성은 프로세서하나에 코어가 여러개 달려서 동시에 여러 프로세스를 처리하는 것을 의미합   니다. 스레드란 하나의 프로세스 내에서의 여러 작업 갈래 각각을 의미합니다. 하나의 프로세스 안에서의 특정 자원에 여러개의 스레드가 동시에 접근하면 동시성 문제가 발생할 수 있습니다.

* ### 도커 & k8s란?
  도커는 컨테이너 기반의 가상화 기술입니다. 도커는 하드웨어 레벨 가상화를 하는 VM과는 달리 OS레벨의 가상화를 수행하며 게스트OS를 설치하지 않아도 되어서 가볍다는 장점이 존재합니다. 
  쿠버네티스는 도커로 띄운 수천수만의 컨테이너를 관리하기에 용이하게 해주는 오케스트레이션 작업을 수행합니다. 예를 들어 컨테이너가 예상치 못하게 중지되면 저절로 실행시켜주는 작업을   하거나 요청 트래픽에 대응하여 스케일링 작업등을 수행합니다.
  
* ### AOP란?
  aop는 관점 지향 프로그래밍으로도 불리며 코드를 비즈니스 로직을 실행하는 핵심관심사항과 여러 부분에서 중복적으로 나타나는 횡단관심사항으로 나누어 이용할 수 있게 합니다. 

* ### 트랜잭션이란? 
  DB에 커밋을 할때 일련의 과정을 묶어서 작업의 완전성과 원자성을 보장해주는 단위를 의미합니다. 어떤 트랜잭션에서 여러 작업들 중 한 작업이라도 수행하다가 취소되거나 실패했을 때,       원 상태로 복구(롤백)할 수 있게끔 해주고, 하나의 큰 작업의 논리적인 단위로서 역할을 수행합니다.

* ### DI, IOC란?
  DI는 Dependency Injection의 줄임 말로, 의존성 주입이라는 뜻입니다. 각 클래스의 의존 관계를 Bean 설정 정보를 바탕으로 컨테이너가 자동으로 주입 해줍니다. (생성자 주입, 세터 주입   필드 주입으로 나뉩니다. - 객체의 일관성을 보장하기 위해 생성자 주입을 사용하는 것이 좋습니다.) IOC란 inversion of control의 줄임 말로, 제어의 역전이라는 뜻입니다. 이는 프로그램의 흐름을 개발자가 제어하지 않고, 프로그램이나 프레임워크가 직접 제어를 한다   는 뜻입니다.  
  
* ### 스프링 컨테이너란?
  스프링 빈이 존재하는 공간으로 컨테이너 혹은 IoC컨테이너라고 부릅니다. 컨테이너는 코드의 처리 과정을 위임 받은 독립적인 존재이며 적절한 설정을 해주면, 개발자가 작성한 코드를 스스로 참조한 뒤 알아서 객체의 생성과 소멸 주기(객체의 생애 주기), 의존성 주입등을 관리합니다.
  
* ### ORM이란?
  Object Relational mapping의 줄임말로 하나의 엔티티를 하나의 테이블로 자동 매핑하게 해주는 기술을 말합니다. 대표적으로 JPA가 있습니다.

* ### SOLID 원칙이란?
  좋은 객체 지향 설계를 위한 원칙입니다. 이는 5개로 나눌수 있습니다.
  
  1.SRP(단일책임원칙) - 하나의 클래스는 하나의 역할만 맡아야한다.
  
  2.OCP(개방폐쇄원칙) - 코드는 확장에는 열려있어야하고 수정에는 닫혀있어야한다. (빈 설정 정보 파일 이용하여 하나의 인터페이스를 상속받은 여러개의 클래스를 갈아 끼움 - 다형성, )
  
  3.LSP(리스코프치환원칙) - 자식 클래스는 부모 클래스에서 가능한 행위를 수행할 수 있어야한다.
  
  4.ISP(인터페이스분리원칙) - 인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야한다.
  
  5.DIP(의존성역전원칙) - 구현체(class)보다는 추상체(interface)에 의존해야한다.

* ### DTO와 ENTITY를 분리하는 이유는?
  1.View에서 주고받는 dto 클래스의 구조는 자주 변경이 된다 (UI 요건에 따라서) 하지만, 테이블에 매핑되는 Entity는 그에 비해 변경도 적고, 영향범위도 매우 크다
  
  2.테이블에 매핑되는 정보가, 실제 View에서 주고받는 정보와 다를 수 있다.(이러한 경우에는 변환하는 로직이 필요한데, 같이 쓰게 되면 해당 로직이 Entity에 들어가게 되어서 Entity가 지저분해진다)
  
  3.DB로부터 조회된 모든 Entity를 View로 넘기게 되면, 원하지 않는 정보까지 전달하게 되어 정보 노출에 대한 문제가 생길 수 있고, 이를 막기 위한 비즈니스 로직과는 상관없는 방어 로직들이 생기게 된다

* ### 필터와 인터셉터의 차이는?
  필터(doFilter 이용)와 인터셉터(preHandler, postHandler 이용)는 둘다 모두 컨트롤러 실행 이전, 컨트롤러 실행 이후에 필요한 추가적인 작업들을 수행할때 이용합니다. 
  
  이 두개의 차이점은 다음과 같다. 필터는 스프링 컨텍스트 외부에 존재하여 스프링과 무관한 자원에 대해 동작한다. 하지만 인터셉터는 스프링의 DistpatcherServlet라는 프론트 컨트롤러가 다른 컨트롤러를 호출하기 전, 후로 끼어들기 때문에 스프링 컨텍스트(Context, 영역) 내부에서 Controller(Handler)에 관한 요청과 응답에 대해 처리한다. (출처: https://goddaehee.tistory.com/154)
  
* ### MSA란?
  MSA란 마이크로 서비스 아키텍처(Micro Service Architecture)의 약자로 단일 프로그램을 각 컴포넌트 별로 나누어 작은 서비스의 조합으로 구축하는 방법입니다.
  각 컴포넌트는 서비스 형태로 구현되고 API를 이용하여 타 서비스와 통신하게 됩니다. 각 서비스는 독립된 서버로 타 컴포넌트와 의존성이 없기 때문에 독립된 배포를 하게 됩니다.

  또한 각 컴포넌트가 독립된 서비스로 개발되어있기 때문에 부분적인 확장이 가능합니다. 온라인 쇼핑몰에서 주문 서비스에 트래픽이 증가한다면 해당 서버만 확장을 해주면 됩니다. 물론 이처
  럼 장점만 있는 것은 아닙니다. 모노리틱 아키텍처가 서비스간의 호출이 하나의 프로세스 내에서 이루어지기 때문에 속도가 빠르지만 MSA의 경우 서비스간 호출을 API통신을 이용하기 때문에   속도가 느리고, 통신에 사용하기 위해 값을 데이터 모델로 변환시켜주는 오버헤드가 발생하기도합니다.
  
---------------------------

## 기술파트 외

* ### 왜 다른 곳이 아닌 이곳에 지원했는지?

* ### 하고싶은 활동이 있는가?

* ### 잘 따라오지 못하는 팀원이 있다면 어떻게할 것인가?

* ### 갈등을 겪었을때 어떻게 해결할 것인가? 갈등을 해결해 본 경험이 있는가?

* ### 어려움을 극복해본적이 있는가? 

* ### 마지막으로 할말
