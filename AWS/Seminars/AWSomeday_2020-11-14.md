<h1>2020-11-04 AWSome Day</h1>

<h2>AWS Cloud란?</h2>

* 온프레미스 : 서버, 스포리지, 데이터베이스, 애플리케이션을 기업 네트워크에서 접속해서 기업 내에서   
  사용하는 환경

* 클라우드 환경 : 클라우스 서비스 공급자가 제공하는 서버, 스토리지, 데이터베이스, 애플리케이션을   
  인터넷을 통해서 접속하여 사용하는 환경

* AWS는 네트워크로 연결된 하드웨어들을 소유하고 유지 관리한다.
* 고객은 필요한 항목을 프로비저닝하여 사용한다.
  
* 클라우드 배포 모델
  1. 온프레미스(private) : 회사가 소유하고 있는 데이터 센터 혹은 it 리소스를 둘 수 있는 장소에   
     모든 it 인프라를 갖추는 환경
  2. 하이브리드 : 기존 온프레미스와 새롭게 구성하는 클라우드를 같이 사용하는 환경
  3. 클라우드(Cloud All-IN) : 클라우드상에 모든 서비스를 배포하고 사용하는 환경,   
    확장성, 뛰어난 보안 등을 사용할 수 있다. 

* AWS 사용 시의 이점
  * 자본 비용을 가변 비용으로 대체 가능하다. 즉, 사용한 데이터양에 대해서만 비용을 지불할게 되므로   
    필요한 것만 사용할 수 있게 된다. (예측 기반 데이터 센터 투자)

  * 개별 인프라를 사용할 때 보다 소유 비용을 절감하고, 리소스를 같이 구매해서 사용할 수 있기 때문에   
    비용 절감의 혜택을 받을 수 있다.

  * 용량 추정의 불피요 : 필요한 만큼만 사용할 수 있기에 계획을 새울 때 노력이나 시행착오가 줄어든다.   
    기존 온프레미스는 수치를 잡고 서버를 구축하기 때문에 이와 같은 불편함이 없어진다.

  * 속도 및 대응력 향상 : 기존 인프라에서는 직접 구축해야 했던 서비스를 클라우드에서는 이미 제공하기에   
    인프라 구성이 빨라지며, 개발 시 미리 구현된 기능을 조합하여 사용할 수 있게 된다.

  * 데이터 센터 운영 및 유지 관리에 비용 투자 불필요

  * 몇 분 만에 전 세계에 배포 가능 : 클릭 몇번으로 전 세계의 여러 region에 애플리케이션을 손쉽게 배포할 수 있다.   
<hr/>

<h2>AWS 보안</h2>

* 데이터를 안전하게 보관
* 규정 준수 요구 사항 충족
* 비용 절감
* 빠른 확장 가능

* AWS에서 이미 규정을 준수하는 요구 사항을 충족하기에 보안에 있어서 신경쓸 부분이 기존보다 현저히 줄어든다.   
  또한 보안의 확장이 가능하다. (외부 침입 및 안전한 IT 리소스 보호)
<hr/>

<h2>AWS 서비스의 범수</h2>

* 모든 요금은 종량제로 부과된다. 
* 약 140개의 여러 범주 서비스를 고객은 손쉽게 사용할 수 있다.
<hr/>

<h2>AWS Global Infra</h2>

* 전 세계의 22개의 지리적 region에 거쳐 서비스가 제공된다.
* 하나의 Region은 두 개 이상의 가용 영역(데이터 센터)으로 구성되어 있다.
  * ex) ap-northeast-2(서울)은 총 4개의 가용 영역을 가지며, 각 가용 영역은 한 개 이상의   
    데이터 클러스터로 구성된다. 이들은 독립적으로 구성되며, region내에서는 빠른 통신을 위한   
    private network가 구성되어 있다.

* Region 선택 사항 고려 순서
  * Data governance, 법적 요구 사항
  * 고객에 대한 접근성(지연 시간)
  * Region 내에서 사용 가능한 서비스
  * 비용(Region별로 다르다)

* Edge Location : DNS, CDN 등이 위치해있어, 원거리 고객에게 도달하기 위한 시간을 최소화하기 위한 시설
<hr/>

<h2>AWS 관리 인터페이스</h2>

* AWS와 상호작용하기 위한 3가지 방법

  1. AWS Management Console : Web, mobile에서 직관적으로 이해할 수 있는 GUI로, 서비스 사용 가능
  2. AWS CLI : AWS 서비스와 상호작용하기 위한 오픈 소수 도구(Python library로 구축됨)   
    * 환경 : Linux, MacOS, Windows
  3. AWS SDK : AWS가 제공하는 Rest api를 mapping한 상태로 구성되어 있다.   
    위 2개도 이 SDK를 사용하여 구성되어 있다. 현재 많이 사용되는 거의 모든 언어들로 제공되어 있다.   
    다양한 API문서 및 커뮤니티 포럼이 제공되어 필요한 지원을 받을 수 있다.

* AWS CLI, SDK를 사용해 서비스를 자동화하여 설정할 수 있다.
<hr/>

<h1>AWS 시작하기</h1>

<h2>Infra 구축 - EC2</h2>

* Amazon EC2 : EC2는 클라우드에서 안전하게 사용할 수 있는 컴퓨팅 파워를 제공하는 가상 머신이다.   
  온프레미스 서버와 비교했을 때 다음과 같은 이점이 있다.
  * `탄력성` : 원할 때 인스턴스를 실행하고 종료할 수 있다. 한 번에 여러개의 인스턴스를 동시 생성할   
    수도 있고, 자동으로 확장 및 축소되게 하여 비용의 최소화가 가능하다.
  * `제어` : 사용자의 needs에 따라 제어가 가능하다
  * `유연성` : 여러 종류의 인스턴스를 필요에 따라 선택하여 사용할 수 있다.   
    추후에 인스턴스의 타입을 변경할 수도 있다.
  * `통합` : ELB, RDS 등의 다양한 AWS의 서비스들과 통합이 가능하다. 이로써 더 쉽게 아키텍쳐를   
    구현하고 다른 AWS의 서비스를 편리하게 사용할 수 있다.
  * `가용성` : EC2 사용 중 이벤트의 발생 시간을 최소화할 수 있다.
  * `보안` : 여러 단계의 보안 요소를 포함하는 Amazon VPC에서 작동하기에 안전하게 사용 가능하다.
  * `저렴한 비용` : 탄력적으로 인스턴스의 실행 및 종료가 가능하기에 온프레미스에 비해 당연히 자원을 효율적으로   
    사용할 수 있으며 Auto-Scaling을 사용하면 트래픽이 몰리는 상황에 대한 대비가 가능하다.
  * `용이성` : AWS의 모든 작업은 SDK, CLI, Console로 제공되기에 쉽게 사용이 가능하다.

* EC2의 인스턴스 유형
  * t2, m3, m4, m5 : 범용(균형잡힌 성능)
    * 사용 사례 예시 : 웹 사이트, 웹 애플리케이션 개발, 코드 repo, 비즈니스 앱
  * c3, c4, c5 : 컴퓨팅 최적화(뛰어난 CPU 성능)
  * g3, p2, p3
  * r5, r5a, r4, x1e, x1
  * i3, i3en

* C5n : 컴퓨팅 최적화 인스턴스
  * Intel XEON 확장 가능 프로세서 탑재
  * C5에 비해 33% 증가된 메모리 공간 제공
  * 최대 크기에서 100Gbps, 최소 크기에서 25Gbps의 대역폭 제공

* R5 : 메모리 최적화 인스턴스
  * 메모리 : vCPU 비율이 8:1인 메모리 최적화 인스턴스
  * 최대 25Gbps 네트워크 대역폭
  * 2.5GHz Intel XEON 확장형 프로세서

* z1d : 특별한 워크로드를 위한 고성능 인스턴스
  * 8:1의 메로리 : vCPU 비율
  * 관계형 DB 수행하기에 적합

* M5 : 차세대 번용 인스턴스 
  * 웹, 애플리케이션 서버, DB, 앱 개발 환경 등을 구축하기에 좋다.
  * 균형잡힌 성능을 제공한다.

* T3 : 차세대 범용 인스턴스
  * 필요한 경우 성능을 순간 확장할 수 있는 기능을 제공한다.
  * 트래픽 대응이 뛰어나며, 비용 절감이 가능하다.

* 플랫폼의 선택 : AMI(Amazon Machine Image) 선택
  * OS뿐 아니라 앱 서버, 앱 정보등을 모두 포함할 수 있다.
<hr/>

<h2>데이터 저장</h2>

* Amazon Elastic Block Store(Amazon EBS)
  * 인스턴스용 영구 블록 스토리지
  * 자동 복제를 통해 보호된다.
  * 상이한 드라이브 유형(SDD, HDD)
  * 몇 분만에 볼륨의 확장 또는 축소가 가능하다.
  * Snapshot 가능
  * 암호화 사용 가능

* Amazon S3
  * 데이터는 버킷 내에 객체로 저장된다. (하나의 객체의 크기는 최대 5TB)
  * 무제한 스토리지(버킷)
  * 99.999999% 내구성
  * 버킷 및 객체에 대한 세분화된 액세스
  * 객체에 대해 빠르고 내구성과 가용성이 높은 Key기반 액세스 가능
  * 데이터를 저장 및 검색하도록 구축된 객체 스토리지
  * 파일 시스템이 아니다.
  
  * 일반 시나리오
    * 백업 및 스토리지
    * 애플리케이션 호스팅
    * 미디어 호스팅
    * 소프트웨어 전송

  * 단순한 스토리지 버킷이 아닌, 데이터전송 비용 부과를 요청자 또는 데이터 버전에 따라 요청할 수 있다.
    * 요청자 지불
    * 버전 관리
    * 정적 웹 사이트 호스팅
    * 객체 수명 주기 관리
    * 사진 등의 정적 컨텐츠를 보관하기에 용이하다.

  * 버킷 생성 후 public object로 생성하고, 제공된 링크를 이용하면 버킷에 업로드한 파일을 받아볼 수 있다.
    * `Open` 버튼을 누르면 public이 된다.
    * 접근 통제는 `permissions` 탭에서 확인 가능하다.

* Amazon S3 Glacier
  * Amazon S3 의 스토리지 클래스 중 하나로 선택 가능하다.
  * 매우 저렴한 데이터 보관 및 장치 백업 가능
  * Amazon Glacier에 Amazon S3 컨텐츠의 수명 주기 보관을 구성할 수 있다.
  * S3의 데이터 보관 시에 사용 가능하다.
  * 사용 사례(오래동안, 보존의 가치가 있는 데이터들을 보관한다.)
    * 미디어 자산 워크플로
    * 의료 정보 아카이빙
    * 과학적 데이터 스토리지
    * 디지털 보존
    * 마그네틱 테이프 대체
    * 규지 및 규정 준수를 위한 아카이빙

  * Vault 잠금 정책 : 한번 저장된 데이터가 일정 시간이 지나면 수정 불가능하도록 막는 정책
    * Vault는 한번 잠기면 수정 불가하다.
<hr/>

<h2>데이터 보호 : VPC</h2>

* VPC : Amazon Virtual Private Cloud
* VPC 내에서 EC2와 같은 AWS 인스턴스를 생성하여 사용할 수 있다.
* VPC내에 퍼블릿 서브넷 또는 기업을 위한 프라이빗 서브넷을 구축해서 사용할 수 있다.
* 보안그룹 : 인바운드, 아웃바운드 트래픽을 제어할 수 있는 가상 방화벽의 역할
  * 모든 인바운드 요청 허용 : `0.0.0.0/0`으로 지정
  * 특정 규칙에 다른 보안 그룹 ID를 넣을 수도 있다. 이를 보안 그룹의 Chaining이라 한다.   
    조금 더 편리한 트래픽 관리가 가능하다.
  * `허용` 규칙만 해당, `거부` 규칙은 없다.
  * 기본값 : 인바운드 트래픽 허용 X, 모든 아웃바운드 트래픽 허용
  * 상태 저장 : 허용된 인바운드 트래픽의 응답을 허용
<hr/>

<h1>클라우드 구축</h1>

<h2>단순 서버 및 스토리지 그 이상</h2>

* 마이그레이션은 기업이 소유하는 IT자원의 형태나 앱의 구조에 따라 다르지만, 기본적으로 네개의 특징을 띈다.
  1. 프로젝트 단위 단계: 프로젝트를 단일 클라우드에서 동작시켜본다.
  2. 클라우드 기초 인프라 구축 단계
  3. 마이그레이션 단계
  4. 혁신 단계
<hr/>

<h2>초기 프로젝트의 개선</h2>

* 인스턴스 문제 : 성능, 확장성, 사용률
* 데이터베이스 문제 : 인프라 관리, 패치, 확장성
* 관리 문제 : 모니터링, 오류 발생에 대비, 배포
<hr/>

<h2>AWS 리소스 모니터링</h2>

* Amazon CloudWatch : AWS의 여러 리소스를 모니터링해주는 서비스
  * 모니터 기능 : AWS에서 실행중인 애플리케이션 모니터링 가능
  * 수집 및 추적 기능 : 표준 지표, 사용자 지정 지표
  * 경보 기능 : 알림 전송, 고객이 정의한 규칙대로 자동 변경

  * 대부분의 AWS 서비스는 Cloudwatch에 정보를 보내며, 고객은 지표를 사용하여 모니터링할 수 있다.
  * ex.) 임계치 설정 후 초과 시 CloudWatch 경보를 사용하여 관리자에게 연락하도록 할 수 있다.

  * 이점 
    * 단일 플랫폼에서 모든 지표에 액세스 가능
    * 애플리케이션, 인프라, 서비스 전반에 대한 가기성 유지
    * 평균 해결 시간 감소 및 총 소유 비용 향상

* Amazon EC2 Auto Scaling이 필요에 따라 용량을 조절해준다.
  * 급증 시에 확장
  * 피크 외의 시간에 축소
  * 비정상 인스턴스 교체
  * 사용한 만큼만 비용 지불

* EC2 Auto Scaling의 동적 조정
  * 애플리케이션 로드 지표 선택
  * 조건부 또는 일정 예약으로 설정
  * CloudWatch로 사용(선택 사항)
  * 인스턴스 개수의 최대치 및 최소치를 설정할 수 있다.
  * 손상된 인스턴스를 중단 없이 자동 교체할 수 있다.
  * 여러 가용 영역에서 용량 밸런싱이 가능하다.

* Elastic Load Balancing : 여러 대상에 자동으로 트래픽을 분산시켜 준다.
  * 고가용성
  * 상태 확인
  * SSL/TLS 종료
  * 운영 모니터링
<hr/>

<h2>DB 서비스의 배포</h2>

* Amazon EC2에 직접 DB를 설치해서 사용할 수도 있고, RDS를 사용할 수도 있다.

* Amazon RDS(Relational Database Service)란?
  * 클라우드에서 관계형 DB의 설정, 운영 및 확장을 손쉽게 해주는 데이터베이스 서비스
  * 간편하게 확장 가능
  * 자동 소프트웨어 패치
  * 백업 자동화
  * 다중 AZ 배포
  * 자동 호스트 교체
  * 보관중인 데이터와 전송중인 데이터의 암호와 지원

* Amazon Aurora란?
  * Mysql, Postgresql과 호환
  * 표준 MySQL 보다 최대 5배 빠른 속도
  * Amazon S3로 지속적인 백업

* Amazon DynamoDB란?
  * 어떤 규모에서든 빠르고 유연한 NoSQL 데이터베이스 서비스
  * 완전 관리형
  * 지연 시간이 짧은 쿼리
  * 세분화된 액세스 제어
  * 지역 및 전역 옵션
  * NoSQL이므로 확장 및 축소에 대해 다운 타임이 발생하지 않는다.
  * 주로 서버리스 웹 애플리케이션, 모바일 백엔드 등에 주로 사용된다.

* AWS Database Migration Service란?
  * 데이터베이스를 AWS로 빠르고 안전하게 마이그레이션해주는 서비스
  * 일회성 및 동기화도 가능하다.
<hr/>

<h2>배포 자동화</h2>

* AWS CloudFormation란?
  * 모든 클라우드 인프라 리소스를 모델링 및 프로비저닝할 수 있다.
  * 예시 : `CloudFormation Designer로 템플릿 파일 작성(YAML/JSON)` --> `인터넷 게이트웨이` --> `웹 서버`

* 인프라 관리 없이 배포할 때에는 AWS Elastic Beanstalk를 사용할 수 있다.
  * 애플리케이션 코드 업로드
  * 서비스 처리사항 : 리서스 프로비저닝, 로드 밸런싱, 자동 조정, 모니터링
  * 서비스 규모를 수백만 사용자로 확장하는 애플리케이션 지원

* AWS Elastic Beanstalk의 기능
  * 광범위한 애플리케이션 플랫폼 선택
  * 다양한 애플리케이션 배포 옵션
  * 모니터링
  * 애플리케이션 상태 관리
  * 모니터링, 로깅 및 추적
  * 관리 및 업데이트, 규모 조정, 사용자 지정 및 규정 준수
<hr/>

<h2>네트워크 서비스</h2>

* Amazon Route 53란?
  * 도메인 명 등록 및 모니터링 기능 제공

* Amazon Elastic File System(Amazon EFS)란?
  * 동적 탄력성
  * 확장 가능한 성능
  * 공유 파일 스토리지
  * 완전 관리형
  * 비용 효율성

* AWS Lambda : 서버 없이 코드 실행
  * 코드를 작성하고 Lambda에 업로드하고, 이벤트 소스에서 코드가 트리거되도록 설정하면 트리거된 경우에만   
    Lambda에서 코드를 실행한다. 사용한 컴퓨팅 시간에 대해서만 비용을 지불한다.
  * 이점
    * 여러 프로그래밍 언어 지원
    * 완전히 자동화된 관리
    * 내결함성 기본 제공
    * 여러 함수의 오케스트레이션 지원
    * 사용량에 따라 요금 지불

* Amazon CloudFront란?
  * 빠르고 안전한 글로벌 컨텐츠 전송 네트워크(CDN)
  * 캐시를 사용하여 데이터를 전송하는 것을 지원한다.
<hr/>

<h1>요금 기본 사항 및 아키텍쳐</h1>

* AWS의 요금 지불 방식
  *  사용량에 따라 지불 = 사용한 만큼만 지불
  *  예약을 통한 비용 절감
    * Reserved Instance 사용 시 동일한 온디맨드 용량에 대해 최대 75% 절감 가능
    * 절감율 : 전체 선결제 > 부분 선결제 > 선결제 X 
  *  사용량이 많을수록 비용 절감

* 요금 개념
  * 컴퓨팅 : 시간/초당 청구, 인스턴스 유형에 따라 다름
  * 스토리지 : 일반적으로 GB당 청구
  * 데이터 전송 : 아웃바운드 요금은 집계하여 청구, 인바운드는 무료(일부 예외), 일반적으로 GB당 청구

