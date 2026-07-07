# 오늘의 AI 개념: 중국산 오픈소스 LLM의 기업 확산(Chinese Open-Weight LLM Enterprise Adoption)

> 작성일: 2026-07-08 · 분류: trend

## 한 줄 정의

DeepSeek·Qwen·Z.ai 같은 중국산 오픈소스 LLM(대형언어모델)이 훨씬 낮은 가격에 비슷한 성능을 내면서, 미국 기업들이 OpenAI·Anthropic 같은 폐쇄형 모델에서 이쪽으로 이동하는 흐름이 빨라지고 있다.

## 쉬운 설명

지난 1년 사이 프론티어 모델(가장 앞선 성능의 상용 AI 모델)의 토큰 사용 요금이 여러 미국 AI 랩에서 상승했다. 동시에 DeepSeek·Qwen(알리바바)·Z.ai 같은 중국 기업들이 소스코드와 가중치를 공개하는 오픈소스·오픈웨이트 모델을 잇달아 내놓으면서, 비슷한 성능을 훨씬 낮은 비용에 구현할 수 있는 대안이 생겼다.

비유하자면 지금까지는 성능 좋은 정품 소프트웨어 하나만 있던 시장에, 소스코드까지 공개된 무료 대안이 등장해 기능은 거의 비슷한데 사용료만 5분의 1 수준으로 낮아진 상황과 비슷하다. 처음에는 "그래도 정품이 낫겠지"라며 버티던 기업들도, 사용료 차이가 매달 수억 원 단위로 벌어지자 계산기를 다시 두드리기 시작했다.

기존에 다룬 "GPT-5.6 정부 승인 파트너 제한 출시"가 최상위 폐쇄형 모델의 성능 경쟁에 관한 소식이었다면, 이 흐름은 성능이 아니라 비용과 접근성을 기준으로 기업들이 실제 채택 모델을 바꾸고 있다는 시장 구조의 변화를 다룬다는 점에서 다르다.

## 구체 예시·사례

AI 업무 자동화 스타트업 Lindy는 2026년 6월 자사 트래픽 전체를 Anthropic Claude 모델에서 DeepSeek로 옮겼다. Lindy CEO는 "비용 곡선이 바닥까지 무너졌다"며 이 전환으로 향후 몇 달 안에 수백만 달러를 절감할 것이라고 밝혔다. Airbnb CEO 브라이언 체스키는 자사가 알리바바의 Qwen 모델에 크게 의존하고 있으며 "빠르고 고품질이며 비용 효율적"이라고 밝혔고, OpenAI 모델은 프로덕션에서 많이 쓰이지 않는다고 언급했다.

가격 격차는 구체적인 수치로도 확인된다. GPT-5.5 기준 출력 토큰 100만 개를 생성하는 데 30달러가 드는 반면, DeepSeek V4-Pro는 2026년 5월 가격 인하 이후 같은 물량에 0.87달러가 든다. Z.ai의 GLM 5.2는 한 에이전틱 벤치마크에서 Anthropic Opus 4.8과 1퍼센트포인트 이내로 근접한 성능을 내면서 비용은 약 5분의 1 수준이라는 평가도 나왔다.

## 왜 지금 중요한가

OpenRouter(여러 AI 모델을 중개하는 플랫폼)에서 미국 기업이 중국산 AI 모델에 쓰는 토큰 비중은 2026년 2월 8일 이후 매주 30%를 넘어섰고, 최고치는 46%까지 올랐다. 이는 지난 12개월 평균치인 11%에서 크게 뛴 수치다.

브루킹스 연구소 연구원은 "중국산 AI 모델은 AI 비용이 치솟는 지금 미국 기업들에 특히 매력적"이라며, "예전에는 미국 기업들이 모델과 무관하게 AI 도입을 우선시했지만, 지금은 비용에 훨씬 민감해졌다"고 짚었다. 우버는 연간 토큰 예산을 4개월 만에 소진했고, 세일즈포스는 올해 Anthropic에 지불할 비용이 3억 달러에 이를 것으로 알려지는 등, 비용 압박이 기업들의 실제 의사결정을 바꾸고 있다는 근거들이 잇따르고 있다.

- [Chinese AI models are gaining ground with U.S. companies as OpenAI, Anthropic costs surge (CNBC, 2026-07-07)](https://www.cnbc.com/2026/07/07/chinese-ai-models-costs-us-openai-anthropic.html)
- [China's Zhipu is closing in on top U.S. AI models with Anthropic and OpenAI held back (CNBC, 2026-06-26)](https://www.cnbc.com/2026/06/26/china-zhipu-z-ai-open-source-anthropic-openai.html)
- [Low-cost Chinese AI models like DeepSeek gain traction in the U.S. (Rest of World)](https://restofworld.org/2026/when-americans-choose-chinese-ai/)

## 회계법인 AI 직무 연결 포인트

회계법인이 AI 도구를 도입·자문할 때 총소유비용(TCO) 분석이 더 중요해진다. 같은 업무를 처리하는 데 모델별로 토큰당 요금이 수십 배 차이 날 수 있으므로, 감사·재무 데이터 분석용 AI를 선택할 때 성능 벤치마크뿐 아니라 실제 사용량 기준 비용 시뮬레이션을 함께 제시하는 역량이 자문 업무의 경쟁력이 된다.

다만 중국산 모델을 감사·재무 데이터 처리에 쓰려면 데이터가 어느 국가 서버에 저장·처리되는지, 클라이언트의 기밀 정보 보호 규정과 상충하지 않는지를 먼저 확인해야 한다. 일부 기관은 데이터 주권·보안 우려로 이런 모델의 사용 자체를 금지하고 있으므로, 회계법인이 클라이언트에 AI 도구를 추천할 때는 비용 절감 효과와 데이터 거버넌스 리스크를 함께 검토해야 한다.

또한 이런 비용 경쟁은 회계법인 자체의 AI 도입 예산 계획에도 영향을 준다. 특정 벤더 모델에 감사 워크플로를 강하게 결합시키기보다, 여러 모델을 상황에 맞게 바꿔 쓸 수 있는 구조를 갖춰두면 향후 가격 변동에 유연하게 대응할 수 있다.

## 핵심 용어·논쟁

- **오픈웨이트(Open-weight) 모델** — 모델의 학습된 가중치 파일을 공개해 누구나 내려받아 자체 서버에서 구동할 수 있는 모델. 소스코드까지 공개하는 완전 오픈소스와는 구분되기도 한다.
- **토큰(Token)** — LLM이 텍스트를 처리하는 최소 단위. 과금은 보통 입력·출력 토큰 수를 기준으로 매겨진다.
- **TCO(총소유비용)** — 도입 비용뿐 아니라 운영·유지 전체 기간의 비용을 합산한 개념.
- **에이전틱 벤치마크(Agentic Benchmark)** — 모델이 단순 대화가 아니라 도구 사용·다단계 작업 수행 능력을 평가하는 성능 지표.
- **데이터 주권(Data Sovereignty)** — 데이터가 저장·처리되는 국가의 법률에 따라 관할권이 달라진다는 원칙.

논쟁 지점: 중국산 오픈소스 모델의 가격 우위가 실제 총소유비용까지 낮추는지에 대해서는 이견이 있다. 자체 인프라 구축·운영 비용, 보안 검증 비용까지 고려하면 API 요금만 비교하는 것보다 격차가 줄어들 수 있다는 지적과, 데이터 주권·수출통제 리스크가 가격 이점을 상쇄할 수 있다는 우려가 함께 제기되고 있다.

## 자료 깊이 읽기

### Chinese AI models are gaining ground with U.S. companies as OpenAI, Anthropic costs surge (CNBC) — 영어 / 텍스트 / 중급
CNBC가 2026년 7월 7일 보도한 기사로, 이 주제의 핵심 데이터가 담겨 있다. OpenRouter에서 미국 기업의 중국산 모델 토큰 사용 비중이 2026년 2월 8일 이후 매주 30%를 넘어섰고 최고 46%까지 올랐다는 수치, 그리고 지난 12개월 평균이 11%였다는 비교 기준을 제시한다. Lindy가 6월 전체 트래픽을 Claude에서 DeepSeek로 옮기며 수백만 달러를 절감하게 됐다는 사례와, Z.ai GLM 5.2가 Anthropic Opus 4.8과 근접한 벤치마크 성능을 5분의 1 비용에 낸다는 평가를 함께 다룬다. 브루킹스 연구소 연구원의 코멘트를 인용해 "미국 기업들이 AI 도입 자체보다 비용에 민감해지는 국면"으로 전환됐다고 짚는다. 성능 경쟁이 아니라 비용 경쟁이 시장 점유율을 바꾸고 있다는 이 기사의 핵심 프레임은 이 주제를 이해하는 가장 직접적인 근거다.

### China's Zhipu is closing in on top U.S. AI models with Anthropic and OpenAI held back (CNBC) — 영어 / 텍스트 / 중급
같은 CNBC가 2026년 6월 26일 보도한 관련 기사로, 중국 AI 기업 Zhipu(Z.ai)의 성능 추격을 다룬다. 미국 랩들의 최상위 모델 출시가 늦어지는 사이 중국 오픈소스 모델들이 성능 격차를 빠르게 좁히고 있다는 점을 지적하며, 이 흐름이 단순 가격 경쟁을 넘어 기술 경쟁력 자체의 문제로 번지고 있다고 짚는다. 앞선 CNBC 기사(7월 7일자)가 가격·채택 데이터에 집중한다면, 이 기사는 그 가격 경쟁이 가능해진 배경인 성능 추격 자체를 조명한다는 점에서 상호 보완적이다.

**그 외 참고**
- [Low-cost Chinese AI models like DeepSeek gain traction in the U.S. (Rest of World)](https://restofworld.org/2026/when-americans-choose-chinese-ai/) — 영어, 텍스트, 중급
- [DeepSeek V4's permanent price cut upends enterprise AI (VentureBeat)](https://venturebeat.com/infrastructure/how-deepseeks-radical-architecture-is-shattering-silicon-valleys-token-moat) — 영어, 텍스트, 중급
- [오픈소스 LLM 씬의 라이징 스타! 'DeepSeek'을 알아보자 (Turing Post 한국어판)](https://turingpost.co.kr/p/deepseek-model) — 한국어, 텍스트, 초급

## 자가 점검 질문

1. 중국산 오픈소스 LLM의 가격 우위가 실제 총소유비용(TCO) 절감으로 이어지려면 어떤 조건이 충족돼야 하는가?
2. 회계법인이 클라이언트에 AI 모델을 추천할 때, 비용 효율성과 데이터 주권·보안 리스크 중 무엇을 우선 기준으로 삼아야 하는가?
3. 특정 벤더 모델에 감사 워크플로를 강하게 결합시키는 전략과, 여러 모델을 유연하게 바꿔 쓰는 전략은 각각 어떤 상황에서 유리한가?
