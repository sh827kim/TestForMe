# TestForMe
# 업무용 프로그램 개발 방안

## A 고객사 시스템의 채널 확대 및 사용자 증가에 따라 발생하는 인증 및 세션 관리 문제 해결을 위한 인증 방식 개선 방안

- 추정 내용
  - 기존 방식이 세션쿠키 방식 또는 DB 기반 세션 인증 방식일 것으로 추정. 
  - jwt 토큰과 같이 유지 시간을 좀 증가시킬 수 있고, in-memory 캐싱 방식으로 전환하는 방안을 서술하면 될 것 같단 추측이 듦 

### 키워드

| 분류            | 키워드                               | 참조링크                                                     |
| --------------- | ------------------------------------ | ------------------------------------------------------------ |
| 인증 방식       | OAuth2.0                   | https://blog.naver.com/mds_datasecurity/222182943542<br />https://guide.ncloud-docs.com/docs/b2bpls-oauth2 |
|                 | OpenID Connect             | https://hudi.blog/open-id/                                   |
|                 | SAML                       | https://www.okta.com/kr/blog/2020/09/what-is-saml/           |
|                 | 다단계 인증(MFA)           | https://www.silverfort.com/ko/glossary/multi-factor-authentication-mfa/ |
| 세션 관리       | 세션 타임아웃 관리         | https://life-is-potatoo.tistory.com/56                       |
|                 | 세션 스토리지 (예: Redis)  |                                                              |
|                 | 세션 하이재킹 방지         | https://livelyoneweek.tistory.com/67                         |
| 보안 및 암호화  | JWT                        | https://velog.io/@yena1025/JWT-%ED%86%A0%ED%81%B0%EA%B3%BC-%EB%AC%B4%EC%83%81%ED%83%9C%EC%84%B1Stateless<br />https://velog.io/@strangehoon/%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%98%EB%A9%B4-JWT%EB%A5%BC-%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C |
|                 | SSL/TLS 암호화             |                                                              |
|                 | 비밀번호 해싱 (예: bcrypt) |                                                              |
| 사용자 경험(UX) | SSO                        | https://aws.amazon.com/ko/what-is/sso/                       |
| 확장성 및 성능  | API 게이트웨이             | https://wildeveloperetrain.tistory.com/205                   |
| 분산 아키텍처   | 분산 세션 관리             | https://developheo.com/bunsan-seobeo-hwangyeongeseoyi-sesyeon-gwanrireul-wihan-3gaji-bangbeob/ |



## A 고객사 비즈니스 유연성과 성능 관점에서 상품을 관리하기 위한 데이터 모델을 새롭게 설계하고 설계 사유 제시

- 추정 내용
  - Monolithic RDB 에 굉장히 묶여있는 데이터 모델일 것으로 추정. 
  - 이론적인 MSA 와 같이 분리된 데이터 모델을 설계하면 될 것 같음

### 키워드

| 분류                | 키워드                                 | 참조링크                                                     |
| ------------------- | --------------------------------------- | ------------------------------------------------------------ |
| 데이터 모델링       | 정규화 vs 비정규화            | https://velog.io/@gwichanlee/DB-%EC%A0%95%EA%B7%9C%ED%99%94-%EB%B9%84%EC%A0%95%EA%B7%9C%ED%99%94 |
| 성능 최적화         | 인덱스 설계 및 사용           |                                                              |
|                     | 쿼리 최적화                   |                                                              |
|                     | 데이터 파티셔닝               |                                                              |
|                     | 캐싱 계층                     |                                                              |
| 유연성              | 다차원 데이터 모델링          | https://velog.io/@kero88/%EB%8B%A4%EC%B0%A8%EC%9B%90-%EB%AA%A8%EB%8D%B8%EB%A7%81 |
|                     | API를 통한 데이터 액세스      |                                                              |
| 데이터 관리 및 통합 | 데이터 중복 제거              |                                                              |
|                     | 데이터 무결성 유지            |                                                              |
|                     | ETL(Extract, Transform, Load) |                                                              |
| 보안 및 접근 제어   | RBAC                          | https://hello-backend.tistory.com/175                        |
|                     | ABAC                          | 위와 동일                                                    |
| MSA                 | 서비스별 데이터베이스 분리    |                                                              |



## 예약 처리 프로세스와 데이터 모델에서 발생하고 있는 동시성 이슈의 해결 방안 제시

| 분류                         | 키워드                                                   | 참조링크                                                     |
| ---------------------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| 동시성 제어                  | Pessimistic Locking<br />(비관적 락)           | https://sabarada.tistory.com/175<br />https://medium.com/@abhirup.acharya009/managing-concurrent-access-optimistic-locking-vs-pessimistic-locking-0f6a64294db7 |
|                              | Optimistic Locking<br />(낙관적 락)            | 위와 동일                                                    |
|                              | MVCC(Multi-Version Concurrency Control)        | https://mangkyu.tistory.com/53<br />https://velog.io/@onejaejae/DB-MVCC |
|                              | Shared Lock & Exclusive Lock                   | https://velog.io/@haron/DB-Exclusive-lock%EA%B3%BC-Shared-lock%EC%9D%98-%EC%B0%A8%EC%9D%B4 |
| 트랜잭션 관리                | ACID 특성                                      | https://akasai.space/db/about_acid/                          |
|                              | 트랜잭션 격리 수준                             | https://akasai.space/db/about_isolation/<br />https://doooyeon.github.io/2018/09/29/transaction-isolation-level.html |
|                              | 2단계 커밋 프로토콜(2PC)                       | https://velog.io/@jungbumwoo/Two-Phase-commit-%EC%9D%B4%EB%9E%80-2PC |
|                              | 분산 트랜잭션 관리                             |                                                              |
| 데드락 및 레이스 컨디션 해결 | 데드락 탐지 및 해결                            | 하단 별도 표 참조                                            |
|                              | 타임아웃 설정                                  |                                                              |
| 비동기 처리                  | 메시지 큐 시스템                               |                                                              |
|                              | 이벤트 소싱                                    | https://velog.io/@boo105/CQRS-%EC%99%80-Event-Sourcing       |
|                              | CQRS(Command Query Responsibility Segregation) | https://velog.io/@everyhannn/CQRS-Event-Sourcing             |
|                              | 작업 대기열(Job Queue)                         |                                                              |
| 성능 및 최적화               | 캐싱 전략 (Redis, Memcached)                   |                                                              |
|                              | 스케줄러 기반 처리                             |                                                              |
|                              | 데이터 파티셔닝                                |                                                              |
| 분산 처리 및 데이터 관리     | 분산 락 매니저                                 |                                                              |
|                              | 멀티 리전 배포                                 |                                                              |
| MSA                          | 사가 패턴 (Saga Pattern)                       | https://velog.io/@suhongkim98/MSA%EC%99%80-DDD-Saga-Pattern-6 |
|                              | 이벤트 드리븐 아키텍처                         |                                                              |

**데드락 탐지**

| 기법 분류   | 기법                                                         | 설명                                                         |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 데드락 예방 | 자원 할당 그래프(Resource Allocation Graph)        | 자원과 프로세스의 관계를 그래프로 나타내어 데드락 발생 가능성을 사전에 차단하는 방법. |
|             | 은행원 알고리즘(Banker's Algorithm)                | 자원의 최대 요청량을 사전에 고려해, 시스템을 안전한 상태로 유지할 수 있는 경우에만 자원을 할당. |
| 데드락 회피 | Wait-Die Scheme                                    | 오래된 프로세스가 자원을 기다리도록 하고, 젊은 프로세스는 자원을 요청 시 중단하고 재시도. |
|             | Wound-Wait Scheme                                  | 젊은 프로세스가 자원을 요구할 경우, 오래된 프로세스를 중단시키고 자원을 할당. |
|             | 오래된 자원 요청 프로세스 중단(Aging)              | 프로세스의 우선순위를 점진적으로 높여 자원 획득 기회를 증가시켜 데드락을 피하는 방법. |
| 데드락 탐지 | Wait-for 그래프(Wait-for Graph)                    | 시스템 내의 프로세스와 자원 할당 상황을 그래프로 표현하여 주기적으로 사이클을 탐지해 데드락을 확인. |
|             | 데드락 탐지 알고리즘(Deadlock Detection Algorithm) | 시스템 상태를 주기적으로 체크하며, 프로세스 간의 상호 대기 상태를 분석하여 데드락을 탐지. |
| 데드락 해결 | 프로세스 종료(Process Termination)                 | 데드락 상태에 있는 프로세스를 강제로 종료시켜 자원을 회수하는 방법. |
|             | 자원 선점(Resource Preemption)                     | 자원을 점유하고 있는 프로세스로부터 자원을 회수하여 데드락을 해소하는 방법. |
|             | 롤백(Rollback)                                     | 데드락 상태에 있는 프로세스를 이전 안전 상태로 되돌려 데드락 발생 이전의 상태로 복구. |


