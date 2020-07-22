# Keycloak 사용 배경 
###    1.https://spring.io/blog/2019/11/14/spring-security-oauth-2-0-roadmap-update
###    2.스프링 블로그에서 인증서버 지원 중단으로 인증관련 다른 방법을 고민하기 시작
###    3.이후 다시 먼가 계획 하는부분은 계속적 모니터링 필요 
###    4.https://spring.io/blog/2020/04/15/announcing-the-spring-authorization-server
###    5.https://github.com/spring-projects-experimental/spring-authorization-server/blob/master/CONTRIBUTING.adoc
###    6.알아보니 okta(aks) , google oAuth2.0 , Keycloak(redhat opensource) 정도로 추려졌다.
###    7.이후 Keycloak 을 spring boot 기반으로 임베디드하게 사용가능하여 추후 확장 및 이관을 고려하여 keycloak 를 사용하기로 결정
 
# Keycloak 설치 

###    1.spring boot embedded keycloak 검색
###    2.소스코드 받기 https://github.com/Baeldung/spring-security-oauth
###    3.oauth-rest/oauth-authorization-server ( keycloak 내장 시킨 spring boot 기반의 인증서버)
###    4.oauth-resource-server( keycloak의 인가를 받아서 동작되는 리소스서버) 
###    5.oauth-ui-authorization-code-angular 리소스서버에 접근하는 client 어플
# 실행
###    1.Spring boot 기반은 pom.xml 확인시 Java 버전이 13으로되어있으며, 사용하는 버전으로 변경하고 빌드 1.8로 변경했지만 문제가 없음, 어플리케이션 실행시 jpa 기반으로 스키마 자동 생성 , oauth-rest/oauth-authorization-server/src/main/resources/application.yml username password,port변경
###    2.Angular 기반은 src/main/resources/src 까지 접근하여 nom install 
###    3.Keycloak 인증서버 접근 및 설정
###    4.Https://localhost:38083 접근 및 설정한 username , password 로 로그인 
###    5.기본 realms 제거 및 release( my-customer ) 추가
###    6.My-customar 관리자 계정 추가(master realm > user >)  , credentials 에서 페스워드 등록( 등록시 temporary 비활성)
###    7.Mc-customer 만의 권한만 mcadmin에게 할당 (master realm > user > mcadmin > role Mappings > clientRoles> type “my-customer -realm 선택” 이하 롤 모두 선택하여 적용하고 로그아웃 이후 mcadmin 으로 로그인 하여 my-customer relm만 나오는지 확인
###    8.Resource server 에 등록한 my-customer 으로 설정
###    9.Angular 에서 my-customer 기준으로 변경 및 포트 변경
###    10.My-customer 를 이용할 resource 서버를 등록 (client>create>anymal-shop>root url type “http://localhost:8089)
###    11.Access type : confidential 저장후 Credentials 텝에서 시크릿키복사하여 angular에 적용
###    12.myCustomer> client scoops 추가 (read , write , openId) / animal-shop에 client 스코프 반영
###    13.myCustomer > user > add
