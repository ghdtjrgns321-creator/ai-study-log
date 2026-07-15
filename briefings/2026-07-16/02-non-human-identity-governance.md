# 오늘의 AI 개념: 비인간 신원 관리(Non-Human Identity, NHI Governance)

> 작성일: 2026-07-16 · 분류: ai-concept

## 한 줄 정의

사람이 아니라 AI 에이전트나 프로그램이 시스템에 접속할 때도, 사람 직원과 마찬가지로 고유한 신원을 부여하고 권한을 관리해야 한다는 개념이다.

## 쉬운 설명

지금까지 기업의 접근 권한 관리는 "이 계정은 김 대리 것, 저 계정은 박 과장 것"처럼 사람 단위로 이뤄졌다. 그런데 AI 에이전트가 스스로 데이터베이스를 조회하고, 문서를 수정하고, 다른 시스템을 호출하기 시작하면서, 그 에이전트 자체에도 계정과 권한이 필요해졌다. 이것이 비인간 신원(NHI)이다.

비유하면 예전에는 건물 출입증을 사람에게만 발급했는데, 이제는 자율주행 청소 로봇에게도 출입증을 발급해야 하는 상황과 같다. 로봇이 어느 층까지 들어갈 수 있는지, 언제 출입했는지 기록이 남아야 사고가 났을 때 추적할 수 있다.

기존의 서비스 계정(service account)이나 API 키와 다른 점은, AI 에이전트는 스스로 판단해 여러 단계의 작업을 연쇄적으로 수행한다는 것이다. 정적인 API 키 하나로는 "이 에이전트가 지금 무엇을 하려고 이 권한을 쓰는지"를 설명할 수 없어, 업계는 "접근 자체가 아니라 행동을 근거로 실시간 통제한다"는 방향으로 옮겨가고 있다.

기존 IAM(Identity and Access Management, 신원 및 접근 관리)이 사람과 고정된 서비스 계정을 전제로 설계됐다면, 에이전틱 AI 시대의 IAM은 수시로 생성·소멸하고 스스로 다른 시스템을 호출하는 신원을 다뤄야 한다는 점에서 근본적으로 다시 설계되고 있다.

## 비슷한 것과 비교

| 구분 | 사람 계정(Human Identity) | 기존 서비스 계정/API 키 | 비인간 신원(NHI, 에이전트) |
|---|---|---|---|
| 수명 주기 | 입사~퇴사, 관리 체계 성숙 | 장기간 고정, 관리 소홀하기 쉬움 | 작업 단위로 생성·소멸, 수량 폭증 |
| 권한 판단 | 사람이 요청 시 검토 | 발급 시 고정 | 실시간·행동 기반 판단 필요 |
| 감사 추적 | 로그인 기록 위주 | 키 사용 로그 | 어떤 작업을, 왜 수행했는지까지 필요 |

사람 계정 관리 체계를 그대로 에이전트에 적용하면 규모와 속도를 감당하지 못하므로, 별도의 거버넌스 체계를 새로 설계해야 한다는 것이 선택 기준이다.

## 왜 지금 중요한가

Cloud Security Alliance는 비인간 신원 거버넌스를 에이전틱 AI 시대의 "가장 위험한 보안 공백"으로 규정했다. 관련 업계 조사에 따르면 비인간 신원과 AI 에이전트 수가 사람 계정의 100배를 넘어설 수 있다고 보고 있으며, 조직의 91%가 이미 AI 에이전트를 쓰고 있지만 이를 관리할 체계가 잘 갖춰진 곳은 10%에 불과하다. 자사 AI 에이전트가 접근한 데이터를 추적·감사할 수 있는 기업은 52%에 그쳐, 나머지 절반 가까이는 컴퓨터 침해 발생 시 조사할 근거 자체가 없는 상태다.

- [The Non-Human Identity Governance Vacuum – CSA](https://labs.cloudsecurityalliance.org/research/csa-whitepaper-nonhuman-identity-agentic-ai-governance-v1-cs/)
- [AI Agents Are Creating an Identity Security Crisis in 2026 - IANS](https://www.iansresearch.com/resources/all-blogs/post/security-blog/2026/04/19/ai-agents-are-creating-an-identity-security-crisis-in-2026)
- [Agentic AI, non-human identities and the next era of IAM - SailPoint](https://www.sailpoint.com/blog/agentic-ai-and-the-future-of-iam)

## 회계법인 AI 직무 연결 포인트

내부통제 평가(ITGC, IT 일반통제)에서 접근 통제는 핵심 점검 항목인데, AI 에이전트가 재무 시스템이나 ERP를 자동으로 조회·수정하기 시작하면 "누가 이 거래를 승인했는가"라는 질문에 사람 이름이 아니라 에이전트 신원으로 답해야 하는 상황이 생긴다. 이 개념을 모르면 AI 도입 기업의 통제 설계를 제대로 평가할 수 없다.

감사 증거의 신뢰성 측면에서도, AI 에이전트가 어떤 권한으로 어떤 데이터에 접근해 도출한 결과인지 추적 가능해야 감사 증거로 채택할 수 있다. 비인간 신원 관리가 부실한 기업은 이 추적 자체가 불가능한 경우가 많다.

회계법인이 자체적으로 감사 자동화 에이전트를 도입할 때도, 그 에이전트가 클라이언트 데이터에 접근하는 권한 범위와 로그를 어떻게 관리하는지가 정보보안 실사(due diligence)의 새로운 점검 항목이 되고 있다.

## 핵심 용어·논쟁

- 비인간 신원(NHI, Non-Human Identity) — 사람이 아닌 소프트웨어·에이전트에 부여되는 고유 식별 단위
- IAM(Identity and Access Management, 신원 및 접근 관리) — 누가 무엇에 접근할 수 있는지 관리하는 체계
- 액션 기반 통제(actions, not access) — 정적 권한 부여 대신 실시간으로 행동을 근거로 접근을 판단하는 방식
- 신원 확산(identity sprawl) — 관리되지 않는 비인간 신원이 통제 범위 밖에서 급증하는 현상
- 논쟁: AI 에이전트 도입 속도가 거버넌스 체계 구축 속도보다 훨씬 빨라, "먼저 쓰고 나중에 통제한다"는 관행이 보안 공백을 키운다는 우려가 업계 전반에서 제기되고 있다.

## 자료 깊이 읽기

### AI Agent의 신원을 묻다, Non-Human Identity의 진화 — 한국어, 블로그, 중급
Microsoft Azure Korea 기술 블로그로, AI 에이전트를 "기업의 디지털 직원"으로 규정하고 사람 직원처럼 입사(온보딩)부터 퇴사(오프보딩)까지의 생애주기 관점에서 신원과 접근 권한을 관리해야 한다고 설명한다. Entra Agent ID를 예로 들어, 에이전트에게도 사람과 동일한 방식으로 신원을 부여하고 회수하는 절차가 필요하다는 점을 강조한다. 정적 API 키 방식의 한계를 지적하는 대목이 특히 회계법인의 접근 통제 평가에 참고할 만하다.

### The Non-Human Identity Governance Vacuum — 영어, 백서, 고급
Cloud Security Alliance가 발간한 백서로, 비인간 신원을 사람·서비스와 구분되는 별도의 신원 범주로 다뤄야 한다고 주장한다. 수명 주기 관리, 거버넌스, 책임 소재를 사람 계정과 동등한 수준으로 설계해야 한다는 원칙을 제시하며, 조직 대부분이 이 격차를 인지하면서도 대응 체계는 갖추지 못한 현황 통계를 함께 제시한다.

**그 외 참고**
- [AI Identity Security: The Hidden Risks of Non-Human Identities & Agents](https://www.youtube.com/watch?v=RtZREpqwuxI) — 영어, 유튜브, 초급
- [인증을 넘어서: 에이전트 AI 시대의 비인간 신원 관리](https://kr.linkedin.com/pulse/beyond-authentication-governing-non-human-identities-era-dinesh-varma-8tzof?tl=ko) — 한국어, 아티클, 중급
- [Agentic AI, non-human identities and the next era of IAM](https://www.sailpoint.com/blog/agentic-ai-and-the-future-of-iam) — 영어, 블로그, 중급

## 자가 점검 질문

1. 비인간 신원(NHI)이 기존 서비스 계정이나 API 키와 근본적으로 다른 점은 무엇인가?
2. 감사 대상 기업이 AI 에이전트를 도입했다면, 내부통제 평가에서 어떤 항목을 추가로 점검해야 하는가?
3. "먼저 도입하고 나중에 통제한다"는 관행이 만드는 리스크를 회계법인 입장에서 어떻게 설명하겠는가?
