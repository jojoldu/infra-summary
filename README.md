# 웹 개발자를 위한 서버/인프라 용어 정리
처음 웹 개발자로 회사에 입사했을 때 크게 힘들었던 것들이 있다. <br/>
* Javascript 생태계(npm, grunt, require, backbone 등)
* 리눅스 환경 (리눅스 커맨드, 쉘스크립트, Vim 등)
* 서버/인프라 환경

특히나 서버/인프라 환경의 경우 시스템팀과 대화시에 처음 듣는 용어가 너무 많아 부끄러움이 가득했다. <br/>
개발자라고 해서 순수하게 **Application 코드만 개발하면 안된다고** 생각하는 계기가 되었다. <br/>
나와 같은 어려움을 경험하지 않았으면 하는 마음에 관련된 용어들을 정리하려고 한다. <br/>
(**개인적인 생각에** 프로그래밍 언어 가짓수를 늘리는 것보다는 시스템의 전체적인 그림을 그릴수 있는게 더 좋은 것 같다.<br/>
언어는 Java, Javascript, Shell Script까지만 충실히 하고 그외에는 네트워크(HTTP 등), 리눅스 서버, 인프라환경, DB 등에 시간을 할애하는 것을 추천한다.) <br/>
좀 더 내용을 보충하고 싶으신 분들, <br/>
틀린 내용을 수정하고 싶으신 분들 <br/>
모두 마음껏 Pull Request 보내주시면 될것 같다.<br/>

### 용어 정리
* 정적 콘텐츠(static Content), 정적 리소스(Static Resources)
  - 이미지, html, css, js 등과 같이 클라이언트로 반환하는 데이터
  - 내용이 변경하지 않는 것이 특징 (반대로 매 요청마다 변경되는 것을 동적 콘텐츠라 한다.)

* CDN (Content Delivery Network)
  - 콘텐츠를 전송하기 위한 네트워크 시스템
  - 클라이언트 접속 위치를 기준으로 가장 가까운 **캐시** 서버를 선택해서 전달하는 것이 특징
  - 아카마이 (Akamai) 등 상용 서비스가 존재

* 로드 밸런서 (Load Balancer)
  - 클라이언트와 서버사이에서 클라이언트의 요청을 여러 서버로 적절하게 분산하는 것을 **로드 밸런스** 라고 함
  - 로드 밸런스 해주는 장치를 **로드 밸런서**
  - L4 스위치 : TCP 헤더등의 프로토콜 헤더의 내용을 분석해서 서버 결정
  - L7 스위치 : 어플리케이션 계층의 내부까지 분석해서 서버 결정

* LVS (Linux Virtual Server)
  - 여러 리눅스 서버를 하나의 리눅스 서버처럼 사용할 수 있게 해주는 시스템
  - 관례적으로 **리눅스로 만든 로드밸런서** 의 의미로 사용된다.
  - [리눅스 포털 참고](https://www.linux.co.kr/home/lecture/index.php?cateNo=&secNo=&theNo=&leccode=10904)

* OSI 참조 모델 (OSI 7계층 모형)
  - 네트워크 프로토콜 계층을 설명한 모델, 총 7계층으로 나누어져있다.
  - Layer7 (어플리케이션 계층) : HTTP나 SMTP 등
  - Layer4 (트랜스포트 계층) : TCP나 UDP 등
  - [블로그](http://freeism.web-bi.net/tc/657) 참고

* 포워드 프록시 (Forward Proxy)
  - 사용자 PC가 직접 Target 사이트에 접근하는 것이 아니라, 중간 프록시 서버에게 **위임하여** Target 사이트의 데이터를 전달 받는 것을 얘기한다.
  - 즉, **내부에서 외부로 나갈때** 사용되는 프록시
  - 사내 Maven 저장소와 같이 제한된 환경을 제공하고 싶을 경우 사용된다.
  - [참고](https://www.lesstif.com/pages/viewpage.action?pageId=21430345)

* 리버스 프록시 (Reverse Proxy)
  - 사용자 PC가 프록시 서버로 요청하고 프록시 서버가 Target 사이트로 부터 데이터를 가져오는 방식
  - 즉, **외부에서 내부로 들어올때** 사용되는 프록시
  - Nginx 혹은 Apache가 80포트로 요청 받아 Tomcat의 8080포트로 프록시 시키는 경우 등
  - [참고](https://www.lesstif.com/pages/viewpage.action?pageId=21430345)

* 가용성
  - 시스템을 정지시키지 않는 능력의 정도
  - 즉, 가용성이 높다는 말은 **거의 멈추지 않는다** 와 같은 의미

* 확장성
  - 이용자나 규모가 증대됨에 따라 시스템을 확장해서 대응할 수 있는 능력의 정도

* 데몬 (Daemon)
  - 백그라운드에서 지속적으로 실행되면서 특정 작업을 수행하는 프로그램
  - Apache(httpd), Tomcat, Nginx 등

* 스케일 아웃
  - 서버를 여러대 두고 분산함으로써 시스템의 성능을 향상시키는 것
  - 로드밸런서 하위의 웹 서버들 갯수를 늘리는 등을 말함

* 스케일 업
  - 단일 서버의 하드웨어 성능을 향상시키는 것
  - 서버의 메모리를 8G -> 16G로 올리는 등을 말함

* 전송량 (Throughput)
  - 단위 시간당 데이터 전송량
  - 비유하자면 **빨대의 너비가 큰 경우를 전송량이 크다** 라고 한다.

* 지연시간 (Latency)
  - 데이터가 도달할 때까지의 시간
  - 비유하자면 **빨대의 길이가 짧은 경우를 지연시간이 짧다** 라고 한다.

* 부하 (Load)
  - 시스템에 의해 수행되는 작업의 크기 또는 네트워크의 트래픽 수준
  - CPU부하 혹은 I/O 부하등이 있다.
  - "부하가 높다" 라고 하면 현재 성능상 이슈가 발생할 여지가 있다로 해석할 수 있다.

* 페일오버 (Fail Over)
  - 장애 극복 기능
  - 컴퓨터 서버, 시스템, 네트워크 등에서 이상이 생겼을 때 **예비 시스템으로 자동전환** 되는 기능

* 스위치 오버 (Switch Over)
  - 페일오버와 같은 장애 극복 기능
  - **사람이 수동으로 전환** 하는 것

* 엘댑 (LDAP)
  - 디렉토리에 접근하기 위한 경량 프로토콜 (HTTP, FTP와 같은 통신 프로토콜 중 하나)
  - 사용자, 패스워드, 그룹정보 등을 하나하나 설정하기 번거로움을 해결하기 위해 등장
  - 가장 일반적인 사내 인증시스템

* HA (High Availability) Active-standby 구성
  - 무중단 서비스를 가능케하는 클러스터
  - 일반적으로 Active-standby 구성으로 운영
  - Active(활성화) 노드로 운영중, 문제 발생시 Standby(대기) 노드로 페일오버 하도록 구성
  - [gunsystems님 블로그](http://egloos.zum.com/gunsystems/v/6781811) 참고

* 클러스터링
  - 똑같은 구성의 서버들을 **병렬로 연결** 후, 마치 하나의 컴퓨터처럼 사용하는 것
  - 고성능 컴퓨터 1대보다 저사향 컴퓨터 여러대를 클러스터링 하는 것이 더 효과적
  - 기존 시스템의 성능 확장시에도 클러스터링이 좀 더 용이함
  - 보통 로드밸런서와 함께 사용함
  - [타이거범님의 블로그](http://tigerbum.tistory.com/20) 참고

* 레플리케이션
  - [joinc님 블로그](http://www.joinc.co.kr/w/man/12/replication) 참고
   
* 샤딩

### 시스템 운영
