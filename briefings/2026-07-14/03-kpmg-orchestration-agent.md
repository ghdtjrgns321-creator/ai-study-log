# 오늘의 AI 개념: KPMG 감사 오케스트레이션 에이전트(Orchestration Agent)

> 작성일: 2026-07-14 · 분류: audit

## 한 줄 정의

KPMG가 2026년 여름부터 시범 도입하는, 사람 대신 여러 개의 하위 AI 에이전트에게 감사 작업을 나눠 맡기고 지휘하는 상위 AI다.

## 쉬운 설명

오케스트라 지휘자가 각 악기 연주자에게 언제 무엇을 연주할지 지시하듯, 오케스트레이션 에이전트는 어떤 하위 에이전트가 어떤 감사 절차(자산 실사, 매출 프로세스 테스트)를 맡을지 스스로 판단하고 순서를 배정한다. 사람 감사인이 여러 도구를 하나씩 직접 실행하던 기존 방식과 달리, 이번에는 AI가 스스로 작업을 나눠 맡기는 역할까지 수행한다는 점이 다르다.

기존에 KPMG가 써오던 스마트 감사 플랫폼 '클라라(Clara)'는 생성형 AI 기능이 접목되어 문서 검토나 위험 식별을 돕는 도구였다면, 이번 오케스트레이션 에이전트는 그 도구들 위에서 "무엇을, 어떤 순서로, 누구에게" 시킬지를 결정하는 관리자 역할을 맡는다는 점에서 한 단계 위의 자동화다.

## 동작 원리

1. 감사인이 목표를 설정한다(예: 특정 계정과목에 대한 실증절차).
2. 오케스트레이션 에이전트가 필요한 하위 에이전트(문서 검토, 이상거래 탐지, 자산 실사 확인 등 20개 이상)를 선정한다.
3. 각 하위 에이전트가 병렬로 작업을 수행한다.
4. 오케스트레이션 에이전트가 결과를 취합하고 상호 검증한다.
5. 사람 감사인이 최종 판단을 내린다.

이 구조는 마이크로소프트가 2026년 5월 일반 출시한 'Agent 365'라는 에이전트 배포·관리·거버넌스 계층과 결합되어, KPMG 자체 플랫폼인 'KPMG Workbench'가 여러 서비스 영역의 에이전트를 조율하는 방식으로 확장되고 있다.

## 구체 예시·사례

첫 파일럿은 회사 창고나 설비 같은 물리적 자산 가치를 확인하는 실사 업무와, 기업의 매출 프로세스를 테스트하는 업무에 적용될 예정이다. 계획상 2026년 여름 파일럿을 시작해 내년에는 특정 테스트 항목에서 AI 에이전트를 전면 배치하고, 2029년 무렵에는 일상적인 테스트 업무 전체를 에이전트가 수행하는 것을 목표로 삼고 있다.

## 왜 지금 중요한가

KPMG는 2026년 여름부터 오케스트레이션 에이전트를 감사 실무에 시범 적용한다고 밝혔으며, 이는 KPMG가 마이크로소프트와 맺은 5년간 20억 달러 규모의 AI 투자·파트너십의 연장선에 있다. 2026년 6월에는 Agent 365와 Copilot을 KPMG 전 세계 직원 약 27만 6천 명 규모로 확장한다고 발표했다.

- [KPMG to Test Advanced AI Agents in Next Phase for Audits](https://news.bloombergtax.com/financial-accounting/kpmg-to-test-advanced-ai-agents-in-next-phase-for-audits)
- [KPMG and Microsoft scale trusted, enterprise AI agents globally through deployment of Agent 365 and Copilot - Source](https://news.microsoft.com/source/2026/06/09/kpmg-and-microsoft-scale-trusted-enterprise-ai-agents-globally-through-deployment-of-agent-365-and-copilot/)

## 회계법인 AI 직무 연결 포인트

반복적인 실증절차(자산 실사 확인, 거래 테스트)가 자동화되면 감사인은 고위험 판단이 필요한 영역에 더 집중할 수 있게 된다.

오케스트레이션 계층이 감사증거의 추적성과 책임 소재를 어떻게 남기는지가 새로운 감사품질 이슈로 떠오르고 있으며, 이는 하위 에이전트의 판단 근거를 어떻게 문서화하고 검토할 것인가의 문제로 이어진다.

국내 Big4(예: EY한영의 에이전트 감사 전면 도입)와 비교했을 때, 글로벌 대형 회계법인이 여러 에이전트를 조율하는 상위 구조를 먼저 갖추는 접근 방식은 국내 도입 로드맵을 가늠하는 참고 사례가 될 수 있다.

## 핵심 용어·논쟁

- 오케스트레이션 에이전트(Orchestration Agent) — 여러 하위 에이전트의 작업을 배분·조율하는 상위 에이전트.
- 서브에이전트(Sub-agent) — 특정 업무만 담당하는 하위 단위 에이전트.
- Agent 365 — 마이크로소프트가 제공하는 에이전트 배포·모니터링·거버넌스 계층.
- KPMG Workbench — KPMG의 자체 에이전트 조율 플랫폼.

현재 쟁점은 "사람의 개별 검토 없이 여러 에이전트가 처리한 결과를, 감사의견의 근거로 얼마나 인정할 수 있는가"이다. 자동화 범위가 넓어질수록 최종 책임을 누가 지는지, 오류 발생 시 어느 단계에서 걸러졌어야 했는지를 규명하는 절차가 함께 요구된다.

## 자료 깊이 읽기

### KPMG to Test Advanced AI Agents in Next Phase for Audits (Bloomberg Tax) — 영어, 뉴스 기사, 중급
(요약 불가 — 본문 확인 실패. 유료 구독 페이지로 추정되어 검색 결과 요약 수준의 정보만 확인했다.)

### KPMG and Microsoft scale trusted, enterprise AI agents globally (Microsoft Source) — 영어, 공식 발표 자료, 중급
(요약 불가 — 본문 확인 실패. 검색 결과에 노출된 개요 수준으로만 확인했다.)

**그 외 참고**
- [KPMG Plans to Hand Routine Testing Off to AI - Going Concern](https://www.goingconcern.com/kpmg-plans-to-hand-routine-testing-off-to-ai/) — 영어, 회계업계 전문 매체, 입문
- [AI at Scale: How 2025 Set the Stage for Agent-Driven Enterprise Reinvention in 2026](https://kpmg.com/us/en/media/news/q4-ai-pulse.html) — 영어, 공식 보고서, 중급
- ["감사도 AI시대" KPMG, 스마트 감사 플랫폼 '클라라'에 생성형 AI 전격 도입](https://www.hankyung.com/article/202408078173i) — 한국어, 뉴스 기사, 입문

## 자가 점검 질문

1. 오케스트레이션 에이전트 도입이 감사 절차의 어느 단계부터 사람의 개입을 줄이는가?
2. 여러 하위 에이전트가 병렬로 처리한 감사 증거를 취합할 때, 상호 모순되는 결과가 나오면 어떻게 처리해야 하는가?
3. 국내 회계법인이 이 접근 방식을 도입한다면, 국내 감사기준·법규상 어떤 지점에서 제약이 발생할 수 있는가?
