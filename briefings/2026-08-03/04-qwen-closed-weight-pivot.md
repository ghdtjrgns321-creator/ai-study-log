# 오늘의 AI 개념: 알리바바 Qwen의 폐쇄형 전환(Closed-Weight Pivot)

> 작성일: 2026-08-03 · 분류: trend

## 한 줄 정의

중국 오픈소스 LLM 진영을 이끌던 알리바바 Qwen이 2026년 들어 상위 모델(3.7 시리즈)의 가중치(weight) 공개를 중단하고 API 전용 폐쇄형으로 전환하면서, "중국 오픈소스 = 무료 개방"이라는 공식이 흔들리고 있다.

## 쉬운 설명

Qwen은 그동안 메타 Llama와 함께 오픈소스 LLM 진영의 양대 축이었다. 모델 가중치를 Hugging Face에 공개해 누구나 내려받아 자체 서버에서 돌리거나 파인튜닝할 수 있었다. 그런데 2026년 상반기부터 Qwen3.6-Plus, Qwen3.7-Max·Flash 같은 상위 모델들이 잇달아 가중치를 공개하지 않고 API로만 제공되기 시작했다.

비유하면, 지금까지 Qwen은 "레시피(가중치)를 통째로 공개해서 누구나 자기 주방에서 요리할 수 있게 해준 셰프"였다. 이제는 "완성된 요리(API 응답)만 배달해주고 레시피는 안 알려주는" OpenAI·Anthropic식 모델로 갈아타는 중이다. 알리바바는 오픈소스 자체를 완전히 접겠다고 선언한 건 아니고, 하위 모델은 계속 공개하되 최상위 플래그십만 폐쇄한다는 입장이다. 하지만 정확히 언제, 어떤 조건으로 상위 모델을 다시 열지에 대한 공식 약속은 없다.

기존에 다뤘던 "오픈소스 LLM의 기업 확산"(2026-07-08)이 "중국산 오픈모델이 늘어난다"는 흐름이었다면, 이번은 그 흐름 안에서 가장 앞서가던 주자가 방향을 트는 반전이라는 점에서 결이 다르다.

## 구체 예시·사례

2026년 7월 25일 QwenCloud 체인지로그에 조용히 등록되고 7월 27일 OpenRouter에 상장된 Qwen3.7 Flash는, 100만 토큰 컨텍스트와 비전·코딩·웹 검색 기능을 갖춘 모델임에도 Hugging Face에 가중치가 전혀 올라오지 않았다. 가격은 3만 2천 토큰 이하 기준 입력 $0.03·출력 $0.13/1M 토큰이며, 상위 컨텍스트 구간(25.6만~100만 토큰)에서는 $0.20/$0.80까지 올라간다. 같은 계열의 최상위 모델 Qwen3.7-Max는 API 전용 "프로프라이어터리 모델"로 공식 소개되며, 35시간 연속 자율 실행으로 자체 커스텀 칩용 커널 코드를 1,158회 도구 호출·432회 커널 평가를 거쳐 10배 속도 개선까지 스스로 해냈다고 VentureBeat가 보도했다. 이 모델은 Anthropic API 프로토콜을 지원해 Claude Code 같은 외부 하네스에도 그대로 꽂아 쓸 수 있다는 점도 함께 확인됐다.

## 왜 지금 중요한가

Qwen 오픈소스 생태계에는 29만 명 이상의 개발자와 11만 3천 개 이상의 커뮤니티 파생 모델이 얹혀 있었던 만큼, 상위 모델의 폐쇄화는 로컬·온프레미스 LLM을 쓰던 기업·연구자 커뮤니티에 실질적 타격이다. Qwen3.7 Flash는 지난주(2026년 7월 25~27일)에 막 등록된 가장 최신 사례이고, VentureBeat 등 주요 매체가 Qwen3.7-Max의 폐쇄 정책과 자율 실행 능력을 함께 보도하며 이 흐름을 뒷받침한다.

- [Alibaba's proprietary Qwen3.7-Max can run for 35 hours autonomously — VentureBeat](https://venturebeat.com/technology/alibabas-proprietary-qwen3-7-max-can-run-for-35-hours-autonomously-and-supports-external-harnesses-like-anthropics-claude-code)
- [Qwen 3.7 Flash review: a $0.03 vision model with a catch — eesel AI](https://www.eesel.ai/blog/qwen-3-7-flash-review)
- [Alibaba Keeps New Qwen3.5-Omni AI Models Closed, Breaks Open-Source Streak — Winbuzzer](https://winbuzzer.com/2026/03/31/alibaba-qwen35-omni-closed-source-multimodal-ai-xcxwbn/)

## 회계법인 AI 직무 연결 포인트

회계법인이 민감한 고객 재무데이터를 다루는 만큼, 데이터를 외부로 내보내지 않는 온프레미스 LLM 도입을 검토해온 곳들에게 이 흐름은 조달 전략에 직접 영향을 준다. 지금까지는 "성능 좋은 중국산 오픈모델을 사내망에 올려 쓰겠다"는 선택지가 있었지만, 그 선택지의 최상위 옵션이 하나둘 API 전용으로 막히면서 온프레미스 도입 로드맵을 다시 짜야 하는 상황이 생길 수 있다.

또한 API 전용 모델은 데이터가 외부 서버를 거치므로, 감사 증빙·미공개 재무정보를 처리할 때는 해당 벤더의 데이터 보관 정책·국가별 데이터 주권 이슈를 별도로 심사해야 한다. 벤더의 오픈소스 여부가 곧 "사내 통제 가능성"과 직결된다는 점에서, AI 벤더 리스크 평가 체크리스트에 "가중치 공개 여부"를 반영할 필요가 커졌다.

## 핵심 용어·논쟁

- **가중치(Weight)** — 모델의 학습된 파라미터 값 자체. 공개되면 누구나 내려받아 자체 서버에서 실행·수정할 수 있다.
- **폐쇄형/프로프라이어터리 모델(Closed-Weight / Proprietary Model)** — 가중치 없이 API 호출로만 접근 가능한 모델.
- **로컬 LLM 생태계(Local-Weights Crowd)** — 공개된 가중치를 내려받아 자체 인프라에서 모델을 돌리는 개발자·기업 커뮤니티.
- 진행 중인 논쟁: 알리바바는 하위 모델은 계속 오픈소스로 유지하겠다고 밝혔지만, 최상위 플래그십의 폐쇄가 "일시적 상업 전략"인지 "오픈소스 노선의 사실상 종료"인지에 대해 커뮤니티 내 의견이 갈린다. 개발자들은 "3.6 dense가 로컬 LLM 생태계 전체를 끌어올렸다"며 상위 모델 재개방을 요구하고 있지만, 알리바바는 시점을 약속하지 않고 있다.

## 자료 깊이 읽기

### Alibaba's proprietary Qwen3.7-Max can run for 35 hours autonomously — VentureBeat — 영문/기사/중급
Qwen3.7-Max가 35시간 연속 자율 실행으로 자체 커스텀 칩용 코드를 최적화한 사례를 확인했다. 1,158회 도구 호출, 432회 커널 평가를 거쳐 기하평균 10배 속도 개선을 달성했고, Anthropic API 프로토콜을 지원해 Claude Code·OpenClaw 등 외부 하네스에 그대로 연결된다는 점, 그리고 이 모델이 처음부터 "프로프라이어터리"로 소개돼 가중치가 공개되지 않는다는 점을 원문에서 확인했다.

### Qwen 3.7 Flash review: a $0.03 vision model with a catch — eesel AI — 영문/블로그/입문
2026년 7월 25일 QwenCloud 체인지로그 등록, 7월 27일 OpenRouter 상장이라는 구체적 날짜와 함께, 100만 토큰 컨텍스트·구간별 가격($0.03/$0.13부터 $0.20/$0.80까지)을 확인했다. "가중치가 없다", "로컬 LLM을 추적하던 커뮤니티가 이 모델에는 반응하지 않았다"는 지적이 이 폐쇄화 흐름의 실질적 여파를 보여준다.

**그 외 참고**
- [Alibaba Keeps New Qwen3.5-Omni AI Models Closed, Breaks Open-Source Streak — Winbuzzer](https://winbuzzer.com/2026/03/31/alibaba-qwen35-omni-closed-source-multimodal-ai-xcxwbn/) — 영문, 기사, 입문

## 자가 점검 질문

1. Qwen이 상위 모델의 가중치 공개를 중단한 것이 로컬 LLM 생태계에 미치는 실질적 영향은 무엇인가?
2. 회계법인이 AI 벤더를 선정할 때 "가중치 공개 여부"를 리스크 체크리스트에 넣어야 하는 이유는 무엇인가?
3. 알리바바의 이번 전환이 "일시적 상업 전략"인지 "오픈소스 노선의 사실상 종료"인지, 어떤 후속 지표를 보면 판단할 수 있을까?
