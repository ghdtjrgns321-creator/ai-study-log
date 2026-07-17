# 오늘의 AI 개념: COSO 생성형 AI 내부통제 가이던스(COSO GenAI Internal Control Guidance)

> 작성일: 2026-07-17 · 분류: audit

## 한 줄 정의

전 세계 내부통제 기준의 뼈대인 COSO 프레임워크가, 기업이 생성형 AI를 도입할 때 무엇을 통제해야 하는지를 처음으로 공식 정리한 실무 가이드다.

## 쉬운 설명

COSO(Committee of Sponsoring Organizations of the Treadway Commission)는 1985년 미국의 다섯 개 회계·감사 관련 단체가 함께 만든 조직으로, 이 조직이 발표한 내부통제 프레임워크는 전 세계 내부회계관리제도 설계의 기준점 역할을 해왔다. 한국의 내부회계관리제도도 이 COSO 프레임워크를 뼈대로 삼고 있다.

문제는 이 프레임워크가 만들어질 당시에는 생성형 AI 같은 존재가 없었다는 점이다. 사람이 승인하고, 사람이 입력하고, 사람이 검토하는 것을 전제로 설계된 통제 원칙을, AI가 스스로 데이터를 추출하고 거래를 처리하고 업무를 조율하는 상황에 그대로 적용하기는 어려웠다. COSO는 2026년 2월 23일 이 공백을 메우기 위해 "Achieving Effective Internal Control Over Generative AI"라는 가이던스를 발표했다.

비유하면 기존 COSO 프레임워크가 "회사 안의 모든 직원이 지켜야 할 승인·기록·검토 규칙"이라면, 이번 가이던스는 그 규칙을 "AI라는 새로운 유형의 업무 수행 주체"에게 어떻게 적용할지 구체적으로 풀어 쓴 부속 매뉴얼에 가깝다. 기존 원칙을 새로 만든 것이 아니라, 이미 있는 5개 구성요소·17개 원칙을 생성형 AI의 특성에 맞게 다시 해석한 것이 핵심이다.

## 동작 원리

이 가이던스는 두 갈래로 구성된다. 첫째는 생성형 AI가 실제로 수행하는 작업을 데이터 추출·변환(ingestion, transformation), 자동 거래 처리·조정(posting), 업무 흐름 조율(orchestration), 판단 지원(judgment), 모니터링, 규제 인텔리전스, 인간-AI 협업 등 여덟 가지 능력 유형으로 분류하는 "능력 기반 관점(capability-based view)"이다. 각 능력 유형마다 어떤 위험이 발생할 수 있는지, 그 위험을 기존 COSO의 5개 구성요소(통제환경, 위험평가, 통제활동, 정보와 소통, 모니터링)와 17개 원칙 중 어디에 연결해 관리해야 하는지를 매핑한다.

둘째는 실행 로드맵으로, 거버넌스(govern) → 자산 목록화(inventory) → 위험 평가(assess) → 통제 설계(design) → 구현(implement) → 모니터링(monitor)의 여섯 단계로 구성된다. 이 로드맵은 경영진의 실행 계획으로도, 내부감사·IT위험관리·법무 등 준법 부서의 점검 도구로도, 이사회와 외부감사인이 "이 회사가 AI를 어떻게 통합했는지" 이해하는 공통 틀로도 쓸 수 있게 설계됐다.

## 구체 예시·사례

가이던스가 예로 드는 "자동 거래 처리·조정(posting)" 능력 유형을 재무 부서에 적용해보면 이렇다. AI 에이전트가 은행 거래 내역과 회계 시스템의 분개를 자동으로 대조해 불일치 항목을 찾아내고, 정해진 규칙 안에서는 스스로 조정 분개까지 제안하는 상황을 가정하자.

이때 COSO 가이던스가 요구하는 통제는, 그 AI가 어떤 규칙 범위 안에서 조정을 제안할 수 있는지 사전에 정의되어 있는지(통제활동), 제안된 조정이 실제 반영되기 전에 담당자의 승인을 거치는지(통제환경의 권한 구조), AI가 참고한 입력 데이터와 산출한 조정 근거가 기록으로 남는지(정보와 소통), 그리고 이 전체 과정이 주기적으로 재점검되는지(모니터링)다. 사람이 하던 조정 업무를 AI가 대신하더라도, "누가 승인했고 무엇을 근거로 했는지"를 추적할 수 있어야 한다는 원칙은 그대로 유지된다.

## 비슷한 것과 비교

| 구분 | 기존 COSO 내부통제 프레임워크(2013) | COSO 생성형 AI 가이던스(2026) | ISO/IEC 42001 |
|---|---|---|---|
| 대상 | 사람이 수행하는 업무 전반 | 생성형 AI가 관여하는 업무 | 조직의 AI 관리체계(AIMS) 전반 |
| 성격 | 원칙 중심 프레임워크 | 기존 프레임워크의 AI 적용 해설서 | 인증 가능한 국제 경영시스템 표준 |
| 실행 도구 | 5개 구성요소·17개 원칙 | 8개 능력 유형 + 6단계 로드맵 | 요구사항·통제 목록 기반 심사 체계 |
| 주 사용자 | 경영진·감사인 전반 | 내부감사·IT위험관리·외부감사인 | AI 시스템을 운영하는 조직 전체 |

선택 기준은 배타적이지 않다. COSO 가이던스는 이미 COSO 프레임워크로 내부통제를 설계한 조직이 생성형 AI 도입 시 참고할 "해석 지침"에 가깝고, ISO/IEC 42001은 AI 관리체계 자체를 제3자가 인증하는 별도의 표준이라 두 체계는 함께 참고되는 경우가 많다.

## 왜 지금 중요한가

COSO는 2026년 2월 23일 이 가이던스를 발표했으며, Journal of Accountancy·KPMG·Deloitte·IIA(내부감사인협회) 등이 잇따라 이를 다뤘다. Deloitte는 2026년 4월 3일자 Heads Up 자료에서 이 발간물이 "COSO가 자사의 내부통제 프레임워크를 AI 거버넌스 영역으로 공식 확장한 첫 사례"라고 평가했다.

같은 시기 PCAOB의 기존 감사기준(AS 2201, AS 2101)도 2026년 12월 15일 이후 시작하는 회계연도부터 AI가 관여한 통제에 적용되도록 개정되는 등, 규제 측과 기준 제정 측 모두 생성형 AI를 기존 감사·내부통제 체계 안으로 편입시키는 작업이 같은 시기에 겹쳐 진행되고 있다.

- [COSO creates audit-ready guidance for governing generative AI - Journal of Accountancy](https://www.journalofaccountancy.com/news/2026/feb/coso-creates-audit-ready-guidance-for-governing-generative-ai/)
- [COSO releases roadmap on internal control over generative AI - KPMG](https://kpmg.com/us/en/frv/reference-library/2026/coso-releases-roadmap-internal-control-over-generative-ai.html)
- [COSO Releases Publication on Internal Controls Related to Generative AI - Deloitte Heads Up](https://dart.deloitte.com/USDART/home/publications/deloitte/heads-up/2026/coso-internal-controls-generative-ai)

## 회계법인 AI 직무 연결 포인트

회계법인이 클라이언트의 내부회계관리제도(K-SOX 대응 포함)를 평가할 때, 클라이언트가 생성형 AI를 재무보고 프로세스에 도입했다면 이 가이던스의 8개 능력 유형 분류가 곧바로 점검 체크리스트가 된다. "이 회사의 AI가 어떤 능력 유형(추출·조정·판단지원 등)에 해당하는지, 그 유형에 맞는 통제가 설계돼 있는지"를 묻는 것이 실사의 출발점이 된다.

감사인 자신이 AI 감사 도구를 도입할 때도 마찬가지 논리가 적용된다. 회계법인이 자체 AI Accountant나 감사 플랫폼을 쓸 때, 그 AI가 수행하는 절차를 이 6단계 로드맵(거버넌스→목록화→평가→설계→구현→모니터링)에 맞춰 관리하고 있는지가 품질관리 감사(peer review)의 새로운 점검 대상이 될 수 있다.

또한 이 가이던스가 강조하는 "능력 기반 관점"은 감사 위험평가에도 시사점을 준다. 클라이언트가 "AI를 도입했다"고 뭉뚱그려 말하는 대신, 그 AI가 정확히 어떤 능력(데이터 추출인지, 자동 분개인지, 판단 지원인지)을 수행하는지에 따라 위험 수준과 요구되는 통제가 달라진다는 관점은, 감사인이 AI 관련 위험을 평가할 때 쓸 수 있는 실질적인 분류 틀이다.

## 핵심 용어·논쟁

- COSO(Committee of Sponsoring Organizations of the Treadway Commission) — AICPA, IIA 등 5개 단체가 공동 설립한 내부통제 기준 제정 조직.
- 능력 기반 관점(Capability-based view) — AI를 "AI냐 아니냐"가 아니라 "무엇을 하는가(추출·조정·판단지원 등)"로 분류해 위험을 매핑하는 접근법.
- 5개 구성요소·17개 원칙 — COSO 내부통제 프레임워크(2013)의 핵심 골격으로, 통제환경·위험평가·통제활동·정보와소통·모니터링으로 구성.
- 감사 준비된(audit-ready) 가이던스 — 별도의 해석 없이 내부·외부 감사인이 바로 점검 도구로 쓸 수 있도록 설계된 실무 지침.
- 논쟁: 이 가이던스는 새로운 강제 규정이 아니라 기존 COSO 프레임워크의 해설서 성격이라, 법적 구속력 없는 자율 참고 자료에 머문다는 한계가 있다. 조직마다 이를 얼마나 엄격히 적용할지 재량이 크다는 점에서, PCAOB 등 규제기관의 향후 공식 기준 제정 여부가 다음 관전 포인트로 거론된다.

## 자료 깊이 읽기

### COSO creates audit-ready guidance for governing generative AI — 영어, 전문매체 기사, 중급
Journal of Accountancy(AICPA 계열 매체)가 2026년 2월 COSO 가이던스 발표 직후 보도한 기사로, 이 가이던스가 기존 COSO 프레임워크의 5개 구성요소·17개 원칙에 생성형 AI 위험을 매핑하는 방식과, 8개 능력 유형(추출·변환·조정·조율·판단지원·모니터링·규제인텔리전스·인간-AI협업) 분류 체계를 정리한다. 이 로드맵이 경영진의 실행계획이자 내부감사·외부감사인이 공통으로 쓸 수 있는 점검 도구로 설계됐다는 점을 강조하며, 회계·감사 실무자를 주 독자로 삼아 쓰인 기사라 실무 적용 관점에서 읽기 좋다.

### COSO releases roadmap on internal control over generative AI — 영어, 회계법인 공식 리서치 자료, 중급
KPMG의 재무보고 리서치 라이브러리(FRV) 자료로, 6단계 실행 로드맵(govern-inventory-assess-design-implement-monitor)을 회계법인 관점에서 재정리한다. 이 로드맵이 이사회·준법부서·외부감사인 각각에게 어떤 역할을 하는지 구분해 설명하는 대목이, 회계법인이 클라이언트 실사에 이 틀을 어떻게 활용할 수 있는지 가늠하는 데 도움이 된다.

**그 외 참고**
- [COSO Releases Publication on Internal Controls Related to Generative AI - Deloitte Heads Up](https://dart.deloitte.com/USDART/home/publications/deloitte/heads-up/2026/coso-internal-controls-generative-ai) — 영어, 회계법인 공식 자료, 중급
- [COSO Issues Generative AI Guidance - The IIA](https://internalauditor.theiia.org/en/articles/2026/march/coso-issues-genai-guidance/) — 영어, 전문협회 기사, 중급
- [Generative AI Internal Control and COSO - IIA Webinar](https://www.theiia.org/en/content/videos/webinar/2026/achieving-effective-internal-control-over-generative-ai-applying-cosos-new-guidance/) — 영어, 웨비나, 중급

## 자가 점검 질문

1. COSO 생성형 AI 가이던스는 기존 COSO 프레임워크의 5개 구성요소·17개 원칙을 대체하는 것이 아니라 무엇을 하는 문서인가?
2. 클라이언트가 도입한 AI를 "능력 기반 관점"으로 분류해 위험을 평가한다면, 단순 데이터 추출 AI와 자동 분개·조정 AI는 통제 설계에서 어떻게 달라져야 할까?
3. 이 가이던스가 법적 구속력 없는 자율 참고 자료에 머문다는 점은 회계법인의 실사·감사 접근법에 어떤 리스크로 이어질 수 있는가?
