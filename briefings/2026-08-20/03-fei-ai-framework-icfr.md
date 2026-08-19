# 오늘의 AI 개념: FEI AI 내부통제 프레임워크(AI Framework: Internal Control Over Financial Reporting)

> 작성일: 2026-08-20 · 분류: audit

## 한 줄 정의

FEI(Financial Executives International) 산하 CCR(Committee on Corporate Reporting)이 2026년 6월 발표한 백서로, 재무보고 과정에 AI를 도입하면서도 SOX 내부회계관리제도(ICFR)의 신뢰성을 유지하기 위해 인간개입 감독·성능 테스트·다중모델 검증·데이터 분석이라는 네 가지 통제 접근법을 제시한다.

## 쉬운 설명

이 프레임워크는 포춘100 및 대형 상장사의 최고회계책임자(CAO)·컨트롤러로 구성된 실무자 그룹이 학계 자문을 받아 직접 작성했다는 점이 특징이다. 규제기관이나 감사기준제정기구가 아니라, 매 분기 재무제표에 서명하고 ICFR 유효성을 직접 평가해야 하는 당사자들이 "우리가 실제로 어떻게 이걸 통제하고 있는가"를 정리한 문서다.

비유하자면 회계법인이 감사기준을 만드는 것과, 감사받는 기업의 재무팀이 "우리 회사에서 실제로 통제가 작동하게 만드는 법"을 스스로 매뉴얼화하는 것의 차이와 비슷하다. FEI 프레임워크는 후자에 해당하며, 그래서 추상적 원칙보다 "오늘 당장 배치할 수 있는 통제 방식 네 가지"라는 실행 단위로 구성돼 있다.

기존 COSO 프레임워크를 대체하는 것이 아니라 그 위에 얹히는 보완재라는 점도 핵심이다. FEI는 이 문서가 2013년 COSO 내부통제 프레임워크에 그대로 맞물리도록(map cleanly) 설계했다고 설명하며, "AI는 ICFR 프로그램에 대한 예외가 아니라 추가 요소(additive)"라는 입장을 명시한다. SEC의 ICFR 정의와 SOX의 합리적 보증(reasonable assurance) 기준 자체는 AI 도입 여부와 무관하게 그대로 유지된다는 뜻이다.

기존에 다룬 COSO의 생성형 AI 내부통제 가이던스(2026-07-17자)나 EU AI Act 12조 기반 감사증적 논의(2026-07-28자)와는 발행 주체와 관점이 다르다. 이 부분은 아래 "비슷한 것과 비교"에서 표로 정리한다.

## 동작 원리

FEI 프레임워크는 하나의 통제 방식을 강요하지 않고, 기업이 AI 시스템의 위험 수준에 맞춰 네 가지 접근법을 개별 또는 조합해서 배치하도록 설계돼 있다.

1. **범위설정(Scoping)** — 재무보고 프로세스에 관여하는 AI 시스템을 식별하고, 그 산출물이 재무제표 계정·주석에 미치는 영향의 중요성(materiality)에 따라 통제 강도를 정한다.
2. **통제 접근법 선택**
   - **인간개입 감독(Human-in-the-Loop)**: AI 산출물이 최종 확정되기 전 전략적 지점에서 사람이 개입해 검증한다. 신뢰도는 가장 높지만 인력·시간 비용이 크다.
   - **성능 테스트(Performance Testing)**: 정답이 알려진 검증된 데이터셋(known baseline)으로 AI 결과의 정확성을 정기적으로 재확인한다. 반복적·유사 거래 처리에 적합하다.
   - **다중모델 검증(Multi-Model Validation)**: 독립적인 챌린저 모델을 병행 운영해 주 모델의 산출물과 교차 비교한다. 다만 두 모델이 같은 유형의 편향을 공유하면 이 방식의 효과가 떨어질 수 있다.
   - **데이터 분석(Data Analytics)**: 시스템 전반의 추세·이상치를 상시 모니터링해 변동을 조기에 포착한다. 커버 범위는 넓지만 개별 건 단위의 정밀도는 상대적으로 낮다.
3. **근거화(Evidencing)** — 어떤 통제를 왜 선택했는지, 검증 결과와 예외 처리 이력을 문서화해 감사인이 신뢰성을 평가할 수 있는 근거로 남긴다.
4. **재평가(살아있는 문서로서의 갱신)** — AI 기술·규제 환경 변화에 맞춰 프레임워크 자체를 주기적으로 개정한다.

## 구체 예시·사례

한 대형 상장사가 매입채무(AP) 자동 분개에 생성형 AI를 도입했다고 가정하자. 이 회사는 FEI 프레임워크의 접근법을 조합해 통제를 설계할 수 있다.

우선 반복적이고 정형화된 거래(예: 정기 공급업체 인보이스)에는 성능 테스트를 적용해, 매월 검증된 샘플 100건을 AI 결과와 대조하며 정확도를 추적한다. 금액이 크거나 이례적인 거래(예: 신규 공급업체·대규모 일회성 지출)에는 인간개입 감독을 걸어, 회계 담당자가 AI 분개 제안을 최종 승인하기 전에 반드시 검토하도록 한다.

동시에 데이터 분석 계층을 깔아 분개 패턴의 월별 변동·이상치를 상시 모니터링하고, 중요 계정에 한해 별도의 검증 모델을 병행 운영하는 다중모델 검증까지 더하면 네 가지 접근법을 계정 위험도에 따라 층위별로 조합한 사례가 된다. 이렇게 남긴 검증 로그·승인 이력·모델 비교 결과가 곧 외부감사인이 확인할 ICFR 통제 증적이 된다.

## 비슷한 것과 비교

| 구분 | FEI AI Framework (2026-06) | COSO 생성형 AI 내부통제 가이던스 (2026-07-17 다룸) | EU AI Act 12조·SOX·TACO 감사증적 (2026-07-28 다룸) |
| --- | --- | --- | --- |
| 발행 주체 | 재무 실무자(CAO·컨트롤러) 그룹, FEI CCR | 내부통제 프레임워크 제정기구(COSO) | 규제기관(EU)·기존 SOX 법제·업계 표준안 |
| 성격 | 실무 배치 가이드(4가지 통제 접근법) | 원칙 기반 프레임워크 해석·적용 지침 | 법적 의무 요건(로그·기록보관) |
| 초점 | ICFR 맥락에서 "어떤 통제를 어떻게 조합할지" | 생성형 AI 리스크를 COSO 5요소에 매핑 | AI 에이전트 행위의 추적 가능성·기록 보존 |
| 독자 | 기업 재무·회계 부서 | 내부통제 설계자·감사인 전반 | 규제 준수 담당자·감사 기술팀 |

세 문서는 경쟁 관계가 아니라 층위가 다르다. COSO가 "왜/어떤 원칙으로" 통제해야 하는지의 상위 프레임워크라면, FEI 프레임워크는 "재무보고팀이 오늘 무엇을 배치할지"의 실행 매뉴얼이고, EU AI Act 12조·TACO 논의는 "그 실행 결과를 어떻게 기록·추적할지"의 증적 요건에 가깝다. 실무에서는 세 가지를 함께 참고해야 빈틈이 없다.

## 왜 지금 중요한가

FEI는 2026년 6월 25일 이 백서를 공식 발표했다. Meta·Walmart·ServiceNow·Alphabet 등 포춘100 기업의 최고회계책임자·컨트롤러가 참여한 CCR이 학계 자문을 받아 작성했으며, "AI가 거버넌스 프레임워크보다 빠르게 재무보고 프로세스에 침투하고 있다"는 격차를 메우기 위한 실무 지침으로 소개됐다. FEI 회장 겸 CEO인 Andrej Suskavcevic은 "AI는 경영진의 내부통제에 대한 근본 책임을 바꾸지 않지만, 그 책임을 어떻게 확인(earn comfort)하는지는 바꾼다"고 밝혔다.

프레임워크는 "살아있는 문서(living document)"로 명시돼 AI 기술·규제 기대치 변화에 맞춰 지속 개정될 예정이다. 다만 이 브리핑 작성 과정에서 FEI 공식 홈페이지(financialexecutives.org)의 보도자료·FEI Daily 페이지는 두 차례 모두 HTTP 403으로 직접 열람이 차단됐다. 이에 따라 사실관계는 FEI가 배포한 PR Newswire 공식 보도자료 전문과 Yahoo Finance 신디케이션(둘 다 FEI 발표문을 그대로 전재)을 1차 대체 출처로 삼아 교차 확인했으며, Cherry Hill Advisory의 독립 해설로 보완했다.

- [FEI Releases "AI Framework: Internal Control Over Financial Reporting" to Help Finance Leaders Adopt AI (PR Newswire, FEI 공식 배포문)](https://www.prnewswire.com/news-releases/fei-releases-ai-framework-internal-control-over-financial-reporting-to-help-finance-leaders-adopt-ai-302810219.html)
- [FEI Releases AI Framework (Yahoo Finance 신디케이션, 인용문·저자명 포함)](https://finance.yahoo.com/technology/ai/articles/fei-releases-ai-framework-internal-120500478.html)
- [FEI Just Wrote the SOX Playbook for AI in Internal Audit (Cherry Hill Advisory 해설)](https://www.cherryhilladvisory.com/risk-register-blog/fei-ai-framework-sox-icfr-internal-audit)
- FEI 공식 페이지(참고용, 직접 열람 실패 — 403): [보도자료](https://www.financialexecutives.org/About-FEI/For-the-Press/2026/fei-ccr-ai-framework-internal-control-financial.aspx), [FEI Daily 해설](https://www.financialexecutives.org/FEI-Daily/June-2026/ai-framework-internal-control-financial-reporting.aspx)

## 회계법인 AI 직무 연결 포인트

회계법인이 클라이언트의 ICFR을 감사할 때, 이 프레임워크는 클라이언트가 AI를 재무보고에 도입한 방식을 이해하는 공통 어휘가 될 수 있다. 감사팀이 클라이언트에게 "AI 산출물에 대해 인간개입 감독을 걸었는지, 성능 테스트 베이스라인이 있는지, 다중모델 검증을 병행했는지, 이상치 모니터링 체계가 있는지"를 이 네 범주로 질의하면, 클라이언트 내부통제 설계의 성숙도를 구조적으로 파악할 수 있다. 특히 이 프레임워크가 COSO 2013과 맞물리도록 설계됐다는 점은, 기존 ICFR 감사 절차(통제 설계 평가→운영 효과성 테스트)에 AI 통제를 끼워 넣기 쉽게 만든다는 의미이기도 하다.

동시에 감사인 입장에서는 이 프레임워크가 제시하는 "근거화(evidencing)" 요구가 곧 요청할 감사증거의 형태를 규정한다. 클라이언트가 인간개입 감독을 주장한다면 검토자 서명·승인 로그를, 성능 테스트를 주장한다면 검증 데이터셋과 정확도 추이를, 다중모델 검증을 주장한다면 두 모델의 비교 결과와 편향 상관관계 점검 이력을 요청해야 한다. 이런 요건이 명문화되면서, 회계법인 신입 인력이 익혀야 할 실무 역량도 "AI 산출물 자체를 재계산"하는 것에서 "AI 통제 설계와 그 증적 체계를 평가"하는 쪽으로 옮겨가고 있다.

다만 이 프레임워크는 미국 실무자 그룹이 미국 SOX·COSO 체계를 전제로 작성한 문서이므로, 국내 K-SOX 감사에 그대로 적용하려면 국내 내부회계관리제도 운영기준과의 정합성 검토가 선행돼야 한다. 삼정KPMG의 'KPMG AI SOX'(2026-08-15자 다룸)처럼 국내 법인이 이미 유사한 AI 기반 내부통제 솔루션을 자체 개발 중인 상황과 비교하며 학습하면, 국내외 접근법의 공통분모(HITL·이상치 탐지 등)와 차이(법정 요건·용어 체계)를 함께 정리할 수 있다.

## 핵심 용어·논쟁

- **ICFR(Internal Control over Financial Reporting)** — 재무제표의 신뢰성 있는 작성을 보장하기 위해 기업이 설계·운영하는 내부통제 체계. SOX 404조가 경영진 평가(404(a))와 감사인 감사(404(b))를 요구한다.
- **CCR(Committee on Corporate Reporting)** — FEI 산하 위원회로, 포춘100·대형 상장사의 컨트롤러·최고회계책임자로 구성돼 회계·보고 이슈에 대한 실무자 관점 지침을 만든다.
- **범위설정(Scoping)** — 감사·통제 대상이 되는 시스템·프로세스·계정의 범위를 정하는 절차. AI 맥락에서는 어떤 AI 시스템이 재무보고에 "충분히 관여"해 통제 대상이 되는지 판단하는 단계다.
- **근거화(Evidencing)** — 통제가 실제로 작동했음을 입증하는 문서·로그·기록을 남기는 행위. 감사인이 통제의 운영 효과성을 판단하는 근거가 된다.
- **살아있는 문서(Living Document)** — 한 번 발행하고 고정되는 것이 아니라, 기술·규제 변화에 맞춰 지속적으로 개정되는 형태의 지침 문서.

현재 진행 중인 논쟁은 "다중모델 검증의 실효성"이다. 서로 다른 벤더의 모델이라도 학습 데이터나 아키텍처가 유사하면 같은 유형의 편향·오류를 공유할 수 있어, 두 모델이 일치한다는 사실만으로 정확성을 보증하기 어렵다는 지적이 실무 해설(Cherry Hill Advisory)에서 제기됐다. 또한 AI 성능이 개선될수록 인간 검토자가 점차 검증을 소홀히 하게 되는 이른바 "자동화 안주(shadow reliance)" 현상도 이 프레임워크가 경계하는 리스크로 거론된다.

## 자료 깊이 읽기

이번 주제는 FEI 공식 페이지 직접 열람이 막혀, 확인 가능했던 텍스트 자료 위주로 구성했다. 적합한 유튜브 영상(SOX·AI 통제 관련)을 검색으로는 찾았으나, 이 환경에서 YouTube 접근 자체가 봇 차단(HTTP 429 및 로그인 요구)으로 막혀 자막을 내려받지 못했다 — 지어내지 않고 텍스트 자료로 대체했다.

### FEI Releases "AI Framework: Internal Control Over Financial Reporting" — 영어/보도자료/중급

FEI가 PR Newswire를 통해 배포한 공식 보도자료 전문이다. 2026년 6월 25일 발표 사실, CCR이 포춘100·대형 상장사 컨트롤러·최고회계책임자와 학계 자문으로 작성했다는 배경, 네 가지 통제 접근법(인간개입 감독·성능 테스트·다중모델 검증·데이터 분석)의 정의, "살아있는 문서"로서 지속 개정될 것이라는 계획이 담겨 있다. FEI 회장 Andrej Suskavcevic의 인용문("AI doesn't change management's fundamental responsibility for effective internal controls — but it does change how we earn comfort over them")도 확인했다.

### FEI Just Wrote the SOX Playbook for AI in Internal Audit (Cherry Hill Advisory) — 영어/블로그 해설/중급

독립 리스크 자문사 Cherry Hill Advisory가 FEI 프레임워크를 실무 관점에서 풀어 쓴 해설이다. 네 가지 통제 접근법을 표로 정리하며 각각의 강점·한계(HITL은 신뢰도는 높으나 비용 집약적, 데이터 분석은 커버 범위는 넓으나 정밀도가 낮음 등)를 짚고, 이 프레임워크가 SEC의 ICFR 정의와 2013년 COSO 프레임워크에 그대로 맞물리도록 설계됐다는 점, "AI는 ICFR에 대한 예외가 아니라 추가 요소"라는 입장을 강조한다. "자동화 안주(shadow reliance)" 리스크와 발행 후 90일 내 실행 과제(AI 인벤토리 파악, 기존 통제 재평가, 감사인과의 조기 협의)도 요약해 실무 착수점을 제시한다.

**그 외 참고**
- [FEI Releases AI Framework (Yahoo Finance 신디케이션)](https://finance.yahoo.com/technology/ai/articles/fei-releases-ai-framework-internal-120500478.html) — 영어, 뉴스, 초급
- FEI 공식 보도자료(직접 열람 실패, 403) — [링크](https://www.financialexecutives.org/About-FEI/For-the-Press/2026/fei-ccr-ai-framework-internal-control-financial.aspx)
- FEI Daily 해설(직접 열람 실패, 403) — [링크](https://www.financialexecutives.org/FEI-Daily/June-2026/ai-framework-internal-control-financial-reporting.aspx)

## 자가 점검 질문

1. FEI 프레임워크가 제시하는 네 가지 통제 접근법 각각의 강점과 한계를 설명할 수 있는가?
2. 회계법인 감사인이 클라이언트에게 AI 통제 증적을 요청할 때, 이 프레임워크의 "근거화" 개념을 어떻게 구체적인 요청 목록으로 바꿀 수 있는가?
3. 이 프레임워크와 COSO 생성형 AI 가이던스, EU AI Act 12조 감사증적 요건은 각각 어느 층위(원칙/실행/기록)를 다루며, 실무에서 왜 셋 다 함께 참고해야 하는가?
