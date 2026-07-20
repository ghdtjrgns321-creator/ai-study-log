# 오늘의 AI 개념: PwC 넥스트 제너레이션 오딧(Next Generation Audit)

> 작성일: 2026-07-21 · 분류: audit

## 한 줄 정의

PwC 글로벌이 감사 계획부터 재무제표 검토까지 감사 전 단계에 AI 도구를 배치해, 2026 회계연도 안에 종단간(end-to-end) AI 자동화를 완성하겠다고 밝힌 감사 혁신 전략이다.

## 쉬운 설명

PwC는 2023년 OpenAI와 3년간 10억 달러 규모의 파트너십을 맺은 데 이어, 자체 "넥스트 제너레이션 오딧" 플랫폼에도 10억 달러를 투자했다. 미국 어슈어런스 혁신 리더 숀 팬슨(Shawn Panson)은 계획·위험평가·워크스루·증거수집·테스트·재무제표 검토 및 타이아웃(tie-out)에 이르는 감사의 모든 단계에 이미 도구가 있거나 곧 생길 것이라고 언급했다.

비유하면 기존 감사가 회계사 여러 명이 각 단계마다 서류철을 손으로 넘겨가며 표본을 뽑아 확인하던 릴레이 경주였다면, 종단간 AI 감사는 출발선부터 결승선까지 하나의 컨베이어 벨트가 자료를 이어 나르고, 회계사는 벨트 위에서 이상 신호가 뜨는 지점마다 판단을 내리는 방식에 가깝다. 표본 대신 전수 데이터를 기계가 훑고, 사람은 그 결과를 검증하고 서명하는 역할로 옮겨간다.

기존 감사 방식과의 차이는 자동화의 범위에 있다. 그동안 회계법인들은 개별 절차(예: 데이터 분석, 이상거래 탐지)에 AI를 부분적으로 붙여왔지만, PwC가 말하는 종단간 자동화는 단계 간 데이터 인계까지 하나의 플랫폼(Maestro)으로 묶어, 위험평가에서 나온 결과가 증거수집 도구로 자동 연결되고 그 결과가 다시 재무제표 검토 단계로 이어지게 설계한다는 점에서 이전의 부분 자동화와 구분된다.

## 동작 원리

PwC의 어슈어런스 플랫폼 Maestro는 위험평가, 데이터 기반 분석, 보안 커뮤니케이션을 하나의 환경에 통합한 AI 네이티브 플랫폼으로 소개된다. 감사 단계별로 AI가 개입하는 흐름은 다음과 같다.

| 단계 | AI 개입 방식 |
|---|---|
| 1. 계획(Planning) | "Simplified Audit for Private Business" 등으로 감사 범위·일정 수립을 자동 지원 |
| 2. 위험평가(Risk Assessment) | Maestro가 데이터를 깊이 탐색해 이상 징후를 부각하고 위험 영역을 좁힘 |
| 3. 워크스루(Walkthrough) | 프로세스 문서를 AI가 요약·정리해 통제 설계 이해를 지원 |
| 4. 증거수집(Evidence Collection) | "Evidence Match"가 문서에서 증거를 자동 추출·대사하고 근거를 기록 |
| 5. 테스트(Testing) | 현금·매출채권·매입채무 등 고빈도 항목을 전수 데이터 기반으로 자동 테스트 |
| 6. 재무제표 검토·타이아웃 | 최종 수치 정합성을 AI가 교차 확인하고 회계사가 최종 판단·서명 |

각 단계는 개별 도구가 아니라 하나의 플랫폼 안에서 데이터가 이어지도록 설계된 점이 핵심이며, PwC는 이를 "사람이 이끌고 기술이 뒷받침한다(human-led, tech-powered)"는 원칙으로 표현한다.

## 구체 예시·사례

Evidence Match를 매입채무(AP) 테스트에 적용하는 상황을 따라가 보면 다음과 같다. 입력은 클라이언트의 회계 시스템에 기록된 매입채무 원장과 공급업체가 보낸 세금계산서·계약서 원본 파일이다.

처리 단계에서 Evidence Match는 어슈어런스 스킬 라이브러리와 연동해 원장의 각 거래 항목과 대응하는 증빙 문서를 자동으로 매칭하고, 금액·날짜·거래처명이 일치하는지 대사한다. 불일치가 발견되면 해당 항목만 예외 목록으로 표시하고, 일치한 항목에는 어떤 증빙과 매칭됐는지 근거를 남긴다.

출력은 전수 대사가 끝난 결과표와 예외 항목 리스트, 그리고 각 매칭의 근거가 기록된 감사 조서(evidence trail)다. 회계사는 표본을 직접 골라 대사하는 대신, AI가 걸러낸 예외 항목에 집중해 실질적 판단을 내리는 방식으로 절차가 재편된다.

## 비슷한 것과 비교

| 구분 | 전통적 감사 방식 | PwC 종단간 AI 감사(Maestro) | 타 빅4 유사 이니셔티브 |
|---|---|---|---|
| 데이터 범위 | 표본 추출 중심 | 전수 데이터 분석 중심 | EY Helix: 저널 엔트리 100% 분석 |
| 단계 간 연결 | 단계별 개별 도구·수작업 인계 | 하나의 플랫폼으로 단계 간 자동 연결 | KPMG Clara: 스마트 감사 플랫폼 + 오케스트레이션 에이전트 |
| 투자 규모 | 해당 없음 | 자체 플랫폼 10억 달러 + OpenAI 파트너십 10억 달러 | KPMG 5년간 20억 달러 투자 발표 |
| 회계사 역할 | 절차 수행 및 표본 검토 | 예외·판단이 필요한 영역에 집중 | Deloitte Zora AI: 엔비디아와 공동 개발한 에이전트 시스템 |

빅4 모두 방향은 유사하지만, PwC는 "감사 전 단계를 잇는 종단간 자동화"를, KPMG는 "오케스트레이션 에이전트가 정형화된 감사를 통째로 실행"하는 데, EY는 "전수 데이터 분석"에 각각 강조점을 두는 것으로 보도된다.

## 왜 지금 중요한가

2025년 11월 보도에 따르면 PwC 미국 어슈어런스 혁신 리더 숀 팬슨은 2026 회계연도(calendar 2026 audits) 안에 종단간 AI 자동화 체계를 갖출 것이라고 밝혔다. 이는 6개월 이내 시점의 목표 시한이라는 점에서 면접 준비 시점(2026년 7월) 기준으로 직접적인 근거가 된다.

같은 시기 PCAOB(미국 상장회사회계감독위원회)는 AI가 감사 품질을 높일 잠재력이 있지만 사람의 판단을 대체할 수 없다는 점을 강조하며, 2026년 검사에서도 AI 활용을 계속 들여다볼 것이라고 밝혔다. 아직 AI 사용에 관한 구속력 있는 규정은 없는 상태로, 감독기관과 대형 회계법인의 AI 자동화 속도가 같은 시기에 나란히 논의되고 있다.

- [PwC expects end-to-end AI audit automation within 2026 - Accounting Today](https://www.accountingtoday.com/news/pwc-expects-end-to-end-ai-audit-automation-within-2026)
- [PwC turns to AI for audit transformation - CFO Dive](https://www.cfodive.com/news/pwc-turns-ai-audit-transformation/650311/)
- [A look at PwC's 'next generation' audit - CFO Brew](https://www.cfobrew.com/stories/2025/11/05/a-look-at-pwc-s-next-generation-audit)
- [AI and the Pursuit of Audit Quality: A Regulatory Perspective - PCAOB](https://pcaobus.org/news-events/speeches/speech-detail/ai-and-the-pursuit-of-audit-quality--a-regulatory-perspective)

## 회계법인 AI 직무 연결 포인트

삼일PwC는 이미 자체 AI Accountant와 Document AI로 연간 20만 시간의 반복 업무 시간을 절감했다고 밝혔고, KSOX AI·Tax Agent 등 내부통제·세무 영역에 특화된 AI 솔루션을 자체 개발해 국내 회계법인 최초로 내부통제 AI 솔루션을 해외에 수출한 사례도 있다. 글로벌 PwC의 Maestro·Evidence Match 같은 종단간 감사 도구가 앞으로 한국 시장에 이식되거나 현지화될 가능성이 높으므로, 이런 글로벌 전략의 구조(단계별 AI 배치, 플랫폼 통합)를 이해해두면 면접에서 "삼일PwC의 AI 전략이 글로벌 전략과 어떻게 연결되는지" 묻는 질문에 구체적으로 답할 수 있다.

면접 준비 관점에서는 단순히 도구 이름을 나열하기보다, "AI가 표본 추출을 전수 검증으로 바꾸면서 회계사의 역할이 절차 수행에서 예외 판단으로 이동한다"는 구조적 변화를 설명하는 것이 중요하다. 삼일PwC의 AX Node가 감사·세무·딜·내부통제 업무 절차와 판단 기준을 온톨로지·지식그래프로 구조화해 AI 에이전트에 주입한다고 밝힌 점도, 글로벌 PwC의 "능력별 단계 배치" 접근과 같은 방향성을 갖는다.

또한 PCAOB가 지적하는 자동화 편향(automation bias)이나 전문가적 회의(professional skepticism) 저하 우려는, 회계법인이 AI 직무 채용 시 지원자에게 "AI 결과를 어떻게 검증할 것인가"를 묻는 배경이 된다. 이 우려를 이해하고 있으면 AI 도구를 다루는 직무라도 감사 품질에 대한 최종 책임은 사람에게 있다는 원칙을 면접에서 명확히 전달할 수 있다.

## 핵심 용어·논쟁

- 종단간(End-to-End) 자동화 — 감사의 개별 절차가 아니라 계획부터 재무제표 검토까지 전 단계를 하나의 흐름으로 자동화하는 것.
- Maestro — PwC의 AI 네이티브 어슈어런스 플랫폼으로, 위험평가·데이터 분석·커뮤니케이션을 통합.
- Evidence Match — 문서와 원장 데이터를 자동 대사하고 근거를 기록하는 에이전트형 증거수집 도구.
- 자동화 편향(Automation Bias) — 감사인이 AI 산출물을 과신해 전문가적 회의를 낮추는 현상.
- 논쟁: AI가 표본이 아닌 전수 데이터를 검토하면 감사 품질이 높아진다는 기대가 있는 반면, PCAOB는 AI 산출물에 대한 과잉 의존과 판단 근거 문서화 부족, 벤더가 모델을 바꾸거나 서비스를 중단할 경우 과거 감사 결과의 재현·검증이 어려워지는 벤더 종속 리스크를 지적한다. 감사 독립성 측면에서도, 감사법인이 특정 AI 벤더(OpenAI)와 대규모 파트너십을 맺는 구조 자체가 향후 규제 검토의 대상이 될 수 있다는 시각이 있다.

## 자료 깊이 읽기

### PwC expects end-to-end AI audit automation within 2026 — 영어, 전문매체 기사, 중급
Accounting Today가 2025년 11월 보도한 기사로, 숀 팬슨의 발언을 인용해 2026 회계연도 안에 계획-위험평가-워크스루-증거수집-테스트-재무제표 검토·타이아웃에 이르는 감사 전 단계에 도구가 배치될 것이라고 전한다. Simplified Audit for Private Business, Evidence Match 등 구체적 도구명과 각 도구가 어느 단계를 맡는지 정리돼 있어 실무 흐름을 파악하기 좋다.

### A look at PwC's 'next generation' audit — 영어, 전문매체 기사, 중급
CFO Brew가 2025년 11월 5일 보도한 기사로, Evidence Match를 "에이전트가 이끄는 증거수집 모듈"로 규정하며 현금·매출채권·매입채무 등 고빈도 항목 테스트에 활용되고 각 매칭에 감사 조서 근거가 남는다는 점을 구체적으로 설명한다. 숀 팬슨의 역할과 발언을 함께 다뤄, 전략 발표의 배경을 이해하는 데 도움이 된다.

### AI and the Pursuit of Audit Quality: A Regulatory Perspective — 영어, 규제기관 연설문, 중급
PCAOB가 공개한 연설 자료로, AI가 감사 품질을 높일 잠재력을 인정하면서도 사람의 판단을 대체할 수 없다는 점, 자동화 편향과 판단 근거 문서화 부족이 새로운 감사 품질 리스크라는 점을 규제기관 시각에서 짚는다. 2026년 시점에 AI 사용에 대한 구속력 있는 규정은 아직 없다는 점도 확인할 수 있어, 회계법인의 자동화 속도와 규제 공백 사이의 긴장을 이해하는 데 유용하다.

**그 외 참고**
- [Financial statement audit services (Next Generation Audit) - PwC Global](https://www.pwc.com/gx/en/services/audit-assurance/next-generation-audit.html) — 영어, 공식 서비스 소개 페이지, 초급
- [Here to listen: PwC's Next Generation Audit - YouTube](https://www.youtube.com/watch?v=PYwUiyweOgk) — 영어, 영상, 초급
- [PwC predicts full end-to-end AI audit automation by 2026 - Accountech Bytes ep135 - YouTube](https://www.youtube.com/watch?v=xcZgyowkgpQ) — 영어, 영상, 초급
- [[AI 워크플로우 혁신] 주요 회계법인, 감사·세무에 AI 심는다 - 디지털데일리](https://www.ddaily.co.kr/page/view/2026051115581496536) — 한국어, 전문매체 기사, 중급

## 자가 점검 질문

1. PwC가 말하는 "종단간(end-to-end) AI 감사 자동화"는 기존의 부분적 AI 도입과 구체적으로 어떤 점에서 다른가?
2. Evidence Match처럼 전수 데이터를 자동 대사하는 도구가 도입되면, 감사인이 직접 수행하는 절차와 판단의 비중은 어느 단계로 옮겨가야 하는가?
3. PCAOB가 지적하는 자동화 편향과 벤더 종속 리스크는, 회계법인이 AI 감사 도구를 설계·운영할 때 어떤 통제 장치로 보완될 수 있는가?
