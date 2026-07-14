# 오늘의 AI 개념: 엔터프라이즈 제너럴 인텔리전스(Enterprise General Intelligence, EGI)와 에이전틱 시뮬레이션 테스팅

> 작성일: 2026-07-15 · 분류: ai-concept

## 한 줄 정의

AI 에이전트를 실제 업무에 투입하기 전에 가상의 기업 환경 안에서 미리 시험해, 실제 상황에서도 일관되게 믿을 수 있는지 검증하는 접근 방식이다.

## 쉬운 설명

범용인공지능(AGI, Artificial General Intelligence)이 "사람 수준의 모든 지적 작업을 해내는 능력"을 목표로 한다면, 엔터프라이즈 제너럴 인텔리전스(EGI)는 목표가 다르다. 한 번 잘하는 것이 아니라, 복잡한 비즈니스 시나리오에서 매번 일관되고 신뢰할 수 있게 성능을 내는 것을 목표로 삼는다.

이 개념을 뒷받침하는 것이 에이전틱 시뮬레이션 테스팅이다. 신입 조종사를 실제 비행기에 바로 태우지 않고 비행 시뮬레이터에서 수백 번 훈련시키듯, AI 에이전트를 실제 고객·실제 데이터에 투입하기 전에 가상의 기업 환경(합성 데이터로 만든 모의 회사)에서 먼저 훈련하고 시험한다.

기존에 다룬 "AI 에이전트 평가(Agent Evals)·LLM-as-a-Judge"가 한 번의 답변이나 짧은 작업 단위를 채점하는 방식이었다면, 에이전틱 시뮬레이션 테스팅은 여러 턴에 걸친 복잡한 업무 시나리오(예: 영업 예측, 서비스 케이스 처리, 견적 산정) 전체를 통째로 시뮬레이션한다는 점에서 범위와 깊이가 다르다.

이 개념이 부상한 배경에는 현실의 실패율이 있다. AI 에이전트가 데모에서는 잘 작동하다가도 실제 배포 단계에서 예상 밖의 방식으로 실패하는 현상을 "들쭉날쭉한 지능(jagged intelligence)"이라 부르는데, 사전 시뮬레이션 검증이 이 간극을 메우는 방법으로 제시되고 있다.

## 동작 원리

1. 실제 기업 데이터 대신 개인정보가 없는 합성 데이터로 가상의 기업 환경(고객, 거래, 상담 이력 등)을 구성한다.
2. 서비스 상담원·분석가·매니저 등 여러 페르소나 역할을 시뮬레이션 안에 배치해, 단발성 응답이 아니라 여러 턴에 걸친 업무 흐름을 재현한다.
3. AI 에이전트가 이 가상 환경에서 실제 시스템에 대한 API 호출까지 포함해 업무를 수행하게 하고, 결과를 정확성·비용·속도·신뢰와 안전성·지속가능성 다섯 가지 지표로 측정한다.
4. 측정 결과를 바탕으로 에이전트가 실제 운영에 투입될 준비가 됐는지(readiness) 판단하고, 부족한 부분은 실제 배포 전에 재훈련하거나 프롬프트·도구를 조정한다.

## 구체 예시·사례

Salesforce AI Research는 CRMArena라는 시뮬레이션 환경을 만들어 이 접근을 구체화했다. 초기 버전은 고객 서비스 단발 응대 시나리오만 다뤘지만, 후속작인 CRMArena-Pro는 영업 예측·서비스 케이스 처리·견적(CPQ) 산정처럼 여러 턴과 여러 에이전트가 얽히는 복잡한 시나리오까지 확장했다.

이런 시뮬레이션이 필요한 이유를 뒷받침하는 수치도 있다. MIT의 한 조사에 따르면 기업의 생성형 AI 파일럿 프로젝트 중 95%가 실제 운영 단계까지 도달하지 못하고 실패했고, Salesforce 자체 연구에서도 대형언어모델 단독으로는 복잡한 업무 시나리오에서 성공률이 35%에 그쳤다고 한다.

## 비슷한 것과 비교

| 구분 | LLM-as-a-Judge(에이전트 평가) | 에이전틱 시뮬레이션 테스팅 |
|---|---|---|
| 평가 단위 | 단일 응답·짧은 작업 | 여러 턴에 걸친 전체 업무 시나리오 |
| 환경 | 정적인 테스트 케이스 | 상호작용 가능한 가상 기업 환경 |
| 측정 지표 | 정답 일치도·품질 점수 | 정확성·비용·속도·신뢰와 안전성·지속가능성 |
| 목적 | 모델·프롬프트 개선 | 실제 배포 준비도(readiness) 판단 |

한 줄로 정리하면, 답변 품질을 빠르게 점검할 때는 LLM-as-a-Judge를, 실제 운영에 투입해도 되는지 판단할 때는 에이전틱 시뮬레이션 테스팅을 쓴다.

## 왜 지금 중요한가

Salesforce AI Research는 2026년 상반기부터 CRMArena-Pro와 EGI 개념을 잇달아 발표하며 "하이프에서 신뢰로(From Hype to Trust)"라는 표현으로 이 접근을 강조하고 있다. VentureBeat는 이를 "AI 에이전트를 위한 비행 시뮬레이터"라고 표현하며, 기업 AI 파일럿의 95%가 실패한다는 MIT 조사 결과와 함께 소개했다.

국내에서도 유사한 흐름이 감지된다. 트릴리온랩스의 모바일 월드모델 'gWorld'가 2026년 ICML 메인트랙에 채택되는 등, "행동을 실행하기 전에 결과를 먼저 시뮬레이션해 검증한다"는 접근이 여러 기업에서 동시에 부상하고 있다.

- [From Hype to Trust: The Role of Agentic Simulation Testing in Advancing the Future of Enterprise General Intelligence](https://www.salesforce.com/news/stories/enterprise-general-intelligence-testing/)
- [Salesforce builds 'flight simulator' for AI agents as 95% of enterprise pilots fail to reach production](https://venturebeat.com/technology/salesforce-builds-flight-simulator-for-ai-agents-as-95-of-enterprise-pilots-fail-to-reach-production)
- [Evaluate LLM Agents for Enterprise Applications with CRMArena-Pro](https://www.salesforce.com/blog/crmarena-pro/?bc=OTH)

## 회계법인 AI 직무 연결 포인트

감사·회계 업무에 AI 에이전트를 투입하기 전에도 같은 논리가 적용된다. 실제 회사의 전표·거래 데이터를 곧바로 넘기기보다, 합성 재무 데이터로 만든 모의 감사 환경에서 에이전트가 이상거래 탐지·계정 대사·문서 검토 같은 여러 턴짜리 업무를 얼마나 일관되게 처리하는지 먼저 검증하는 절차를 설계할 수 있다.

내부통제 관점에서도 연결점이 있다. 에이전트의 배포 준비도를 정확성뿐 아니라 신뢰와 안전성·비용·속도까지 다면적으로 측정하는 방식은, 감사인이 통제를 설계할 때 단일 지표가 아니라 여러 위험 요소를 종합 평가하는 사고방식과 유사하다. 면접에서 "AI 신뢰성 검증"을 이런 다면적 평가 틀로 설명하면 설득력을 높일 수 있다.

다만 감사 데이터는 민감도가 높아 실제 데이터를 시뮬레이션 환경에 그대로 쓸 수 없다는 제약이 있다. 합성 데이터의 현실성이 떨어지면 시뮬레이션에서 좋은 성적을 낸 에이전트도 실제 배포에서는 다르게 행동할 위험이 남는다는 점을 균형 있게 짚어주는 것이 좋다.

## 핵심 용어·논쟁

- 들쭉날쭉한 지능(Jagged Intelligence) — 모델이 어떤 과제는 잘하고 비슷해 보이는 다른 과제는 갑자기 실패하는 현상.
- 배포 준비도(Readiness) — 에이전트가 실제 운영 환경에 투입돼도 되는 수준인지를 나타내는 판단 기준.
- 합성 데이터(Synthetic Data) — 실제 개인정보 없이 인공적으로 만들어 시뮬레이션에 사용하는 모의 데이터.
- CRMArena-Pro — Salesforce가 만든 다중 턴·다중 에이전트 기업 업무 시뮬레이션 벤치마크.

## 자료 깊이 읽기

### From Hype to Trust: The Role of Agentic Simulation Testing — 영어, 공식 블로그, 중급
Salesforce AI Research가 EGI 개념과 에이전틱 시뮬레이션 테스팅의 필요성을 소개하는 원문 발표 자료다. AGI와 달리 EGI가 "일관성과 신뢰성"에 초점을 맞춘다는 점을 명확히 정의하고, 왜 데모 성능과 실제 운영 성능 사이에 큰 간극이 생기는지 설명한다. CRMArena-Pro가 측정하는 다섯 가지 지표(정확성·비용·속도·신뢰와 안전성·지속가능성)를 구체적으로 제시한다. 기업이 AI 에이전트를 실제 배포하기 전 거쳐야 할 검증 단계를 체계화하려는 시도로 읽을 수 있다.

### Salesforce builds 'flight simulator' for AI agents — 영어, IT 전문매체 기사, 초중급
VentureBeat가 Salesforce의 접근을 "AI 에이전트용 비행 시뮬레이터"에 비유해 쉽게 풀어 쓴 기사다. MIT 조사에서 기업 생성형 AI 파일럿의 95%가 운영 단계에 이르지 못했다는 수치와, Salesforce 자체 실험에서 LLM 단독 성공률이 35%에 그쳤다는 수치를 함께 인용한다. 왜 지금 기업들이 "성능이 아니라 신뢰"로 AI 에이전트 평가 기준을 옮기고 있는지 배경을 잘 짚어준다. 실무자가 AI 도입 실패 통계를 인용할 때 참고하기 좋은 자료다.

**그 외 참고**
- [Evaluate LLM Agents for Enterprise Applications with CRMArena-Pro](https://www.salesforce.com/blog/crmarena-pro/?bc=OTH) — 영어, 기술 블로그, 중급
- [Salesforce AI Research Advances the Agentic Enterprise](https://www.salesforce.com/news/stories/ai-research-advances-enterprise-agentic-readiness/?bc=OTH) — 영어, 공식 발표, 중급

## 자가 점검 질문

1. AGI와 EGI는 무엇을 목표로 한다는 점에서 근본적으로 다른가?
2. 에이전틱 시뮬레이션 테스팅을 감사 업무에 도입한다면 어떤 데이터·시나리오로 모의 환경을 구성하겠는가?
3. 시뮬레이션에서 검증된 에이전트라도 실제 배포에서 다르게 행동할 수 있는 이유는 무엇인가?
