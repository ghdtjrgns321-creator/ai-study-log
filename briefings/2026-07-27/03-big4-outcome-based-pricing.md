# 오늘의 AI 개념: 빅4 회계법인의 과금 모델 전환 — 빌러블 아워에서 아웃컴 기반·서비스형 AI로(Outcome-based Pricing & Service-as-a-Software)

> 작성일: 2026-07-27 · 분류: audit

## 한 줄 정의

AI가 감사·세무·자문 업무 시간을 크게 줄이면서, 빅4 회계법인이 "일한 시간만큼 청구하는" 전통적 빌러블 아워(Billable Hour) 모델을 "만들어낸 성과·구독형 AI 서비스만큼 청구하는" 모델로 바꾸려는 산업 전반의 움직임이다.

## 쉬운 설명

빌러블 아워는 회계사·컨설턴트가 일한 시간에 시간당 단가를 곱해 청구서를 끊는, 전문서비스 업계의 오래된 표준 과금 방식이다. 그런데 AI 에이전트가 사람이 몇 시간 걸리던 작업을 몇 분 만에 끝내버리면, 시간을 기준으로 값을 매기는 방식 자체가 무너진다. 일을 잘할수록(AI를 잘 쓸수록) 청구할 시간이 줄어드는 역설이 생기기 때문이다.

비유하면, 예전엔 이삿짐을 몇 시간 걸려 옮겼는지로 요금을 받던 이사업체가, 이제 로봇 팔로 30분 만에 다 옮기게 됐다고 상상하면 된다. 30분치 요금만 받으면 회사는 망하고, 그렇다고 예전 시간 기준을 억지로 유지하면 고객이 "왜 30분 걸린 일에 예전 요금을 내야 하냐"고 항의한다. 그래서 업계는 "이사 자체가 완료됐다"는 결과(아웃컴)나 "로봇 팔을 매달 빌려 쓰는" 구독료로 과금 기준을 바꾸려 한다.

이런 문제의식은 새롭지 않다. 소프트웨어 업계는 이미 SaaS(서비스형 소프트웨어)에서 사용량·성과 기반 과금으로 여러 번 실험해 왔고, 컨설팅업계 일각(예: 매킨지)도 이미 일부 계약을 성과 연동으로 돌린 바 있다. 회계법인의 차이는, 감사 업무 자체가 법정 의무이자 독립성 규정의 적용을 받아 성과 연동 보수 자체가 제한된다는 점에서 세무·자문보다 전환이 더디다는 데 있다.

이 저장소는 이미 KPMG 감사 오케스트레이션 에이전트, KPMG 미국 감사 파트너 약 10% 감원, KPMG Agent 365, 딜로이트 옴니아·Zora, PwC Next Gen Audit·REZE, 삼일PwC AI Accountant·내부통제 자동화 등 개별 제품·조직 개편을 다뤘다. 오늘은 그 제품들이 아니라, 그 제품들이 왜 등장했는지를 설명하는 상위 구조, 즉 "돈을 받는 방식 자체가 바뀌고 있다"는 비즈니스 모델 층위에 초점을 둔다.

## 동작 원리

과금 방식이 바뀌는 흐름은 대략 세 단계로 나뉜다.

| 단계 | 과금 기준 | 특징 |
|------|-----------|------|
| 1. 빌러블 아워 | 투입 시간 × 시간당 단가 | AI로 시간이 줄면 매출도 같이 준다(비효율이 오히려 매출이 되는 구조) |
| 2. 아웃컴 기반(Outcome-based) | 산출된 결과·절감액·리스크 감소분 | "고객이 그 결과에 매기는 가치"를 기준으로 재협상(가치 기반 가격) |
| 3. 구독형·서비스형 AI(Subscription/Service-as-a-Software) | 매달 정액으로 AI 에이전트·플랫폼 접근권 판매 | 사람의 시간이 아니라 에이전트가 처리하는 작업량·범위를 파는 방식 |

실제로는 세 방식이 동시에 섞여 있다. PwC 미국 시니어 파트너 겸 CEO 폴 그릭스(Paul Griggs)는 세무·자문 업무 일부를 시간제 청구가 아닌 AI 도구 기반의 다른 서비스 전달 모델로 전환하고 있다고 밝혔고, PwC AI 리더 댄 프리스트(Dan Priest)는 고객들이 "AI로 얻은 절감액의 몫"을 요구하고 있다고 전했다(Accounting Today, 2026-03-24). PwC 미국 세무 리더 크리샨 찬드라세카르(Krishnan Chandrasekhar)는 "시간은 점점 의미가 없어지고 있다"며, 고객이 그 가치를 어떻게 받아들이는지에 따라 가격을 매기는 가치 기반 접근을 언급했다(Bloomberg Tax, 2026-03-05).

## 구체 예시·사례

가장 구체적인 사례는 KPMG가 자신의 오랜 외부 감사인 그랜트손튼 UK(Grant Thornton UK)에 수수료 인하를 요구한 사건이다. 보도에 따르면 KPMG는 2024년 41만 6천 달러였던 감사 보수를 2025년 35만 7천 달러로, 약 14% 인하하도록 압박했고, 그 근거로 "AI가 비용을 줄였다면 그 절감분이 수수료에 반영돼야 한다"는 논리를 댔다(thefinancestory.com, 2026-02-12). 회계법인이 AI로 남을 압박하던 논리가, 회계법인 자신이 고객 입장이 될 때는 거꾸로 자신에게 돌아온다는 점을 보여주는 사례다.

EY는 세무 부문에 AI 에이전트 약 150개를 배치해 세무 전문가 약 8만 명을 지원하고, 첫 물결에서 세무 컴플라이언스 산출물 300만 건 이상 처리를 목표로 삼았다고 밝혔다(EY 발표, 2025년 초 공개돼 이후 여러 매체가 반복 인용). 다만 이 수치는 2025년 3월 무렵 처음 보도된 것으로, 2026년 기사에서도 새 수치 없이 그대로 재인용되는 경우가 많아 "최신 2026년 성과"로 오인하지 않도록 주의가 필요하다. 별도로 EY는 2026년 4월 7일 공식 뉴스룸을 통해 감사(Assurance) 부문 전체에 에이전틱 AI를 내재화한다고 발표했는데, 이번에는 전 세계 150개국 이상, 감사 전문가 13만 명, 감사 건수 16만 건 규모로 범위가 밝혀졌다(EY 공식 발표, 2026-04-07). 이는 세무 부문 수치와는 별개의, 실제로 2026년에 새로 확인되는 규모다.

KPMG가 자주 인용하는 "AI에 20억 달러를 투자해 120억 달러의 추가 매출을 노린다"는 수치는 사실 2023년 7월 마이크로소프트와의 제휴 확대 당시 발표된 것이다(SiliconANGLE·Axios·VentureBeat, 2023-07-11). 2026년 다수의 2차 보도(예: chatfin.ai 등 정리 블로그)가 이 3년 전 수치를 마치 최신 소식처럼 재인용하고 있어, 벤더 자체 발표 수치이자 갱신되지 않은 옛 수치라는 점을 분명히 해둘 필요가 있다. KPMG가 2025년 6월 선보인 멀티에이전트 플랫폼 Workbench는 당시 기준 에이전트·챗봇 약 50개를 연동했고 약 1,000개를 추가 개발 중이라고 밝혔다(Accounting Today, 2025-06-18). KPMG 글로벌 AI 인력 담당 니얼 클레오버리(Niale Cleobury)는 "주니어가 에이전트를 관리하는 매니저가 되길 원한다"고 밝혔고, 동료 샘 글로디(Sam Gloede)는 "바뀌는 건 조직의 크기가 아니라 모양"이라고 덧붙였다(Business Insider 인용 보도, 2025-11-04).

## 비슷한 것과 비교

| 구분 | 빌러블 아워 | 아웃컴 기반 가격 | 구독형·서비스형 AI |
|------|------------|-----------------|------------------|
| 과금 기준 | 투입 시간 | 산출된 결과·절감액 | 정액 접근권·처리량 |
| AI 효율화의 영향 | 매출 감소로 직결(역설) | AI 성과를 매출로 전환 가능 | 시간과 무관하게 안정적 매출 |
| 감사 업무 적용 | 현재까지 표준 | 독립성 규정으로 제한적 | 도구·플랫폼 사용료 형태로는 가능 |
| 세무·자문 적용 | 축소 추세 | 확대 추세(가치 기반 협상) | 확대 추세(에이전트 카탈로그·구독) |

선택 기준은 한 줄로 요약된다. 법정 감사처럼 독립성이 생명인 업무는 아웃컴 기반이 제약되고, 세무·자문처럼 상대적으로 자유로운 업무일수록 아웃컴·구독형 전환이 빠르다.

## 왜 지금 중요한가

2026년 3월 5일 Bloomberg Tax는 상위 미국 회계법인들이 AI 생산성 향상 앞에서 빌러블 아워를 재설계하고 있다고 보도했고, PwC 세무 리더 크리샨 찬드라세카르의 "시간은 점점 의미가 없어지고 있다"는 발언을 전했다.

2026년 3월 24일 Accounting Today는 회계법인의 약 10%가 빌러블 아워에서 독점적 AI 솔루션 중심 모델로 이동 중이며, 다수 회사가 결과 기반 청구와 자동화로 인력 증원 없이 전달 속도를 높이는 방향을 추진한다고 전했다. PwC 미국 CEO 폴 그릭스, PwC AI 리더 댄 프리스트, PwC 호주 감사(어슈어런스) 리더 수 홀린의 실명 발언이 포함됐다.

2026년 4월 7일에는 EY가 감사 부문 전체에 에이전틱 AI를 내재화한다고 공식 발표해, 개별 도구가 아니라 감사 조직 전체의 작업 방식 자체가 바뀌고 있음을 보여줬다. 같은 시기(2026년 2월) KPMG가 자신의 감사인에게 AI발 수수료 인하를 요구한 사건은, 이 압박이 회계법인들 사이에서도 양방향으로 작동한다는 점을 드러낸다.

- [AI Efficiency Gains Push Accounting Firms to Reimagine Pricing — Bloomberg Tax](https://news.bloombergtax.com/financial-accounting/ai-efficiency-gains-push-accounting-firms-to-reimagine-pricing)
- [AI driving firms, clients to revisit pricing models — Accounting Today](https://www.accountingtoday.com/news/ai-driving-firms-clients-to-revisit-pricing-models)
- [EY launches enterprise-scale agentic AI to redefine the audit experience for the AI era — EY 공식 뉴스룸](https://www.ey.com/en_us/newsroom/2026/04/ey-launches-enterprise-scale-agentic-ai-to-redefine-the-audit-experience-for-the-ai-era)
- [KPMG forced Auditor for a 14% AI Discount...Will the "Billable Hour" die? — The Finance Story](https://thefinancestory.com/kpmg-forced-auditor-for-a-14-ai-discount-will-the-billable-hour-die)

## 회계법인 AI 직무 연결 포인트

국내에서도 유사한 압박이 이미 인력 구조에 반영되고 있다. 국내 4대 회계법인(삼일PwC·삼정KPMG·안진딜로이트·EY한영)의 신입 채용 규모는 2019년 약 1,100명에서 2025년 약 700명으로 30% 이상 줄었고, 삼일PwC 관계자는 "1~3년 차가 담당하던 반복 업무를 AI가 흡수하면서, 회계사가 복잡한 판단·리스크 해석·커뮤니케이션에 집중하는 'AI 협업 전문가'로 성장하고 있다"고 설명했다(한국경제, 2026-05-20). 같은 보도는 영미권 기준 빅4의 AI 기술 역량 요구 채용공고 비율이 전체의 약 7%로, 전통 감사 직무 채용공고(약 3%)보다 두 배 이상 높다고 전했다.

이는 곧 국내 회계법인 지원자에게도 "시간을 파는 사람"이 아니라 "AI가 만든 산출물의 품질과 리스크를 검증하고, 그 결과를 고객에게 어떤 가치로 설명할지 판단하는 사람"으로서의 역량이 채용·평가 기준이 되고 있다는 뜻이다. 면접에서 "AI 도입으로 감사 시간이 줄어든다면 회계법인 매출은 어떻게 되는가"라는 질문을 받는다면, 오늘 다룬 빌러블 아워→아웃컴 기반→구독형 전환 구조를 근거로 답할 수 있다.

다만 이 전환은 아직 완결된 것이 아니라 "진행 중인 실험"이라는 점도 함께 알아둘 필요가 있다. 감사 업무는 독립성 규정 때문에 아웃컴 기반 전환이 더디고, 세무·자문에서도 실제 성과 연동 계약 비중은 아직 크지 않다는 지적이 나온다(McKinsey 사례 기준 전체 매출의 약 25% 수준이라는 분석도 있다). 즉 "빌러블 아워가 완전히 사라졌다"가 아니라 "허물어지기 시작했고, 그 자리를 무엇이 채울지 업계가 실험 중"이라는 서술이 더 정확하다.

## 핵심 용어·논쟁

- **빌러블 아워(Billable Hour)** — 투입 시간에 시간당 단가를 곱해 청구하는 전통적 과금 방식.
- **아웃컴 기반 가격(Outcome-based Pricing)** — 산출된 결과·절감액·리스크 감소분을 기준으로 청구하는 방식.
- **서비스형 소프트웨어(Service-as-a-Software)** — 사람의 노동력이 아니라 AI 에이전트가 수행하는 서비스 자체를 구독·정액으로 판매하는 모델.
- **감사 독립성(Audit Independence) 규정** — 감사인이 피감사회사와 이해관계를 갖지 않도록 하는 규정으로, 성과 연동 보수를 제한하는 근거가 된다.
- **밸류 리키지(Value Leakage)** — 실제 제공한 가치보다 낮은 요율로 청구돼 수익이 새는 현상으로, AI 시대 빌러블 아워의 약점을 지적할 때 쓰인다.

가장 뜨거운 논쟁은 이 전환이 주니어 채용과 경력 경로에 미치는 영향이다. KPMG는 주니어가 "에이전트를 관리하는 매니저"로 성장하길 원한다고 밝혔지만, 동시에 국내외에서 신입 채용 규모 자체가 줄고 있다는 통계도 함께 나온다. AI가 주니어의 반복 업무를 대체하면서 "관리자로 빠르게 성장할 기회"인지 "애초에 진입 인원 자체가 줄어드는 문턱"인지에 대한 평가가 업계 안에서도 갈린다.

## 자료 깊이 읽기

### AI driving firms, clients to revisit pricing models — Accounting Today (2026-03-24)
PwC 미국 시니어 파트너 겸 CEO 폴 그릭스, PwC AI 리더 댄 프리스트, PwC 호주 어슈어런스 리더 수 홀린, General Assembly의 애시 칸나 등 실명 인용을 담은 기사다. 회계법인의 약 10%가 빌러블 아워에서 독점 AI 솔루션 중심 모델로 전환 중이며, 다수 회사가 결과 기반 청구와 자동화를 병행해 인력 증원 없이 전달 속도를 높이는 흐름을 추진한다고 전한다. 고객이 AI발 절감액의 일부를 요구하는 압박과, "AI가 비싸서 서비스가 꼭 저렴해지는 건 아니다"라는 반론도 함께 다룬다.

### KPMG forced Auditor for a 14% AI Discount...Will the "Billable Hour" die? — The Finance Story (2026-02-12)
KPMG가 10년 넘게 자사를 감사해온 그랜트손튼 UK에 AI발 비용 절감을 근거로 약 14%(41.6만 달러→35.7만 달러) 수수료 인하를 요구했다는 사건을 다룬 기사다. 회계법인 교체 위협까지 동원됐다는 보도를 전하며, 이 사례가 법률·컨설팅 등 다른 빌러블 아워 기반 직종에도 경고가 될 수 있다고 짚는다. 다만 빌러블 아워 붕괴나 아웃컴 기반 전환에 대한 직접적 논의는 제한적이다.

### 빅4 회계법인, 감사보다 AI 인력 더 찾는다 / 회계사보다 AI 전문가 더 뽑은 글로벌 빅4 — 한국경제 (2026-05-20)
국내 4대 회계법인의 신입 채용 규모가 2019년 약 1,100명에서 2025년 약 700명으로 30% 이상 줄었다는 통계와, 삼일PwC 관계자의 "AI 협업 전문가로 성장" 코멘트를 전한다. 글로벌 빅4의 영미권 채용공고 중 AI 기술 역량을 요구하는 비율(약 7%)이 전통 감사 직무 요구 비율(약 3%)의 두 배를 넘는다는 통계도 함께 제시한다.

### [486. An AI-Powered Firm of One, KPMG Shuts Down Fed Audits — The Accounting Podcast (YouTube)](https://www.youtube.com/watch?v=LmGzkYJv2Mw)
1인 세무사무소가 기술 예산 70%를 AI에 쓰며 워크페이퍼 작성 시간을 수 시간에서 5분으로 줄인 사례, 실무관리 소프트웨어 Canopy의 "실효 시간당 요율 하락 탐지" 기능, KPMG의 미국 연방정부 감사 부문 철수·자문인력 4% 감원 소식을 다룬다. 다만 본편에는 아웃컴 기반 가격이나 KPMG의 20억달러 투자 관련 논의는 등장하지 않아 배경 참고 자료로만 활용했다. 상세 요약은 `videos/accounting-podcast-486-kpmg-billable-hour.md` 참고.

**그 외 참고**
- [EY launches enterprise-scale agentic AI to redefine the audit experience for the AI era — EY 공식 뉴스룸(2026-04-07)](https://www.ey.com/en_us/newsroom/2026/04/ey-launches-enterprise-scale-agentic-ai-to-redefine-the-audit-experience-for-the-ai-era)
- [AI Efficiency Gains Push Accounting Firms to Reimagine Pricing — Bloomberg Tax(2026-03-05)](https://news.bloombergtax.com/financial-accounting/ai-efficiency-gains-push-accounting-firms-to-reimagine-pricing)
- [Big Four Firms Roll Out AI That Can Handle Routine Tasks Solo — Bloomberg Tax(2025-03-24, EY 150 에이전트·8만 명 수치 최초 보도)](https://news.bloombergtax.com/financial-accounting/big-four-firms-roll-out-ai-that-can-handle-routine-tasks-solo)
- [KPMG to invest $2 billion in AI in expanded partnership with Microsoft — VentureBeat(2023-07-11, 20억달러·120억달러 수치 원출처)](https://venturebeat.com/ai/kpmg-to-invest-2-billion-in-ai-in-expanded-partnership-with-microsoft)
- [KPMG wants junior consultants to ditch the grunt work and hand it over to teams of AI agents — AOL(원출처 Business Insider, 2025-11-04)](https://www.aol.com/news/kpmg-wants-junior-consultants-ditch-135410188.html)
- [Deloitte, EY, PwC, and KPMG scale AI agents across audit, tax, and consulting — Financial World(2025-12-31)](https://www.financial-world.org/news/news/financial/30088/deloitte-ey-pwc-and-kpmg-scale-ai-agents-across-audit-tax-and-consulting/) — 이 기사는 직접 접속(403)이 되지 않아 전문을 확인하지 못했고, 검색엔진이 제공한 요약을 통해서만 "PwC의 매트 우드가 2026년 업무의 초점이 '고객이 그 모델을 뒤집도록 돕는 것'이라고 말했고, EY의 라지 샤르마가 아웃컴 기반 가격과 서비스형 소프트웨어 접근을 언급했다"는 내용을 확인했다. 전문 대조가 안 됐으므로 인용은 참고 수준으로만 다뤘다.

## 자가 점검 질문

1. 빌러블 아워, 아웃컴 기반 가격, 구독형 서비스형 AI는 각각 무엇을 과금 기준으로 삼으며, AI 효율화가 매출에 미치는 영향이 어떻게 다른가?
2. 국내 회계법인에서 감사 업무와 세무·자문 업무의 과금 모델 전환 속도가 다르다면, 그 이유를 감사 독립성 규정과 연결해 설명할 수 있는가?
3. "KPMG가 자신의 외부 감사인에게 AI발 수수료 인하를 요구한 사건"이 보여주듯, 이 전환이 회계법인 자신에게 부메랑으로 돌아올 때 어떤 리스크가 생기는가?
