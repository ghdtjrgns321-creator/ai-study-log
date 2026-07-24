# 오늘의 AI 개념: JetBrains 주니(Junie) 정식 출시(GA) 전환

> 작성일: 2026-07-25 · 분류: agentic-coding

## 한 줄 정의

젯브레인즈가 자사 IDE에 내장된 AI 코딩 에이전트 "주니(Junie)"를 베타에서 정식판으로 전환하면서, 계획 수립부터 실제 디버거를 이용한 디버깅·코드 리뷰까지 맡길 수 있게 됐다.

## 쉬운 설명

Junie는 젯브레인즈(IntelliJ IDEA·PyCharm·WebStorm 등을 만드는 회사)가 만든 AI 코딩 에이전트다. 자연어로 작업을 지시하면 계획을 세우고, 프로젝트 여러 파일을 고치고, 터미널 명령을 실행하고, MCP(모델 컨텍스트 프로토콜, Model Context Protocol) 서버를 호출해 진행 상황을 보고한다.

비유하자면 Junie는 "그 회사에 이미 있는 도구만 쓰는 신입 개발자"에 가깝다. 프로젝트가 원래 쓰던 디버거·빌드 도구·테스트 러너를 그대로 활용하지, 낯선 방식을 새로 추측해서 들이밀지 않는다.

기존에 다룬 클로드 코드(Claude Code)나 GitHub Copilot과 달리, Junie는 특정 IDE에 원래부터 내장돼 있다는 점이 다르다. 별도 터미널 앱을 띄우는 방식이 아니라, 개발자가 매일 쓰는 IDE 화면 안에서 계획·수정·디버깅이 한 번에 이어진다.

## 동작 원리

1. **Plan Mode** — 작업을 시작하기 전에 Junie가 먼저 실행 계획을 구조화해 제시하고, 개발자가 계획 단계에서 방향을 조정할 수 있다.
2. **에이전틱 디버깅** — 코드를 추측으로 고치는 대신, IDE에 내장된 실제 디버거를 실행해 브레이크포인트를 걸고 변수 값을 확인한 뒤 수정한다.
3. **비동기 원격 실행** — 개발자가 다른 작업을 하는 동안 Junie가 원격 환경에서 작업을 계속 진행한다.
4. **프로젝트 인식 코드 리뷰** — 프로젝트 맥락을 아는 상태로 PR·변경사항을 검토한다.
5. **ACP(Agent Client Protocol)로 통합** — 젯브레인즈와 Zed가 공동 개발한 개방형 프로토콜로, IDE와 CLI에서 동일한 Junie 엔진이 동작하며 다른 에이전트(Claude Agent, Codex 등)도 같은 방식으로 연결할 수 있다.
6. **BYOM(Bring Your Own Model)** — 로컬 런타임을 포함해 원하는 모델을 골라 붙일 수 있다.

## 구체 예시·사례

개발자가 "결제 모듈에서 특정 조건일 때 예외가 나는 버그를 고쳐줘"라고 지시하면, Junie는 우선 관련 코드를 훑어 계획을 세우고(Plan Mode), 실제 IntelliJ 디버거로 해당 함수에 브레이크포인트를 걸어 실행을 멈춘 뒤 변수 값을 확인한다. 원인을 특정한 다음에야 코드를 수정하고, 수정 후에는 프로젝트 맥락을 반영해 변경 사항을 스스로 리뷰한다. 이 전 과정이 IDE 화면을 벗어나지 않는다.

## 비슷한 것과 비교

| 구분 | Junie(JetBrains) | Claude Code | GitHub Copilot |
|------|------|------|------|
| 실행 위치 | IDE 내장(+ 별도 CLI) | 주로 터미널 | IDE·GitHub 통합 |
| 디버깅 방식 | IDE의 실제 디버거 직접 조작 | 코드 실행·로그 기반 추론 | 코드 제안·리뷰 중심 |
| 모델 종속성 | LLM-비종속(BYOM 가능) | 앤트로픽 모델 중심 | OpenAI 계열 중심 |
| 프로토콜 개방성 | ACP로 다른 에이전트도 연결 가능 | 자체 생태계 | 자체 생태계 |

이미 젯브레인즈 IDE를 표준으로 쓰는 조직이라면 Junie가 디버거 연동의 이점이 크고, 터미널·CI 환경 중심 워크플로에는 클로드 코드류가 더 맞는다는 것이 선택 기준이다.

## 왜 지금 중요한가

젯브레인즈는 2026년 6월 17일 Junie(CLI 포함)를 베타에서 정식 출시(GA)로 전환했다고 공식 블로그에서 밝혔다. 같은 시기 젯브레인즈는 Zed와 함께 개발한 ACP를 자사 전체 IDE 라인업에 확대 적용한다고 발표했다.

특정 벤더의 에이전트에 코드베이스를 종속시키지 않고 여러 AI 에이전트를 IDE 하나에서 오가며 쓸 수 있게 하는 흐름(ACP)이 동시에 진행되고 있다는 점에서, 이번 GA 전환은 단일 제품 업데이트를 넘어 에이전틱 코딩 도구 생태계의 상호운용성 논의와 맞물려 있다.

- [The JetBrains AI Coding Agent moves to general availability — JetBrains 공식 블로그](https://blog.jetbrains.com/junie/2026/06/junie-coding-agent-out-of-beta/)
- [Agent Client Protocol (ACP): Use Any Coding Agent in Any IDE — JetBrains 공식](https://www.jetbrains.com/acp/)
- [ACP Brings JetBrains on Board — Zed 공식 블로그](https://zed.dev/blog/jetbrains-on-acp)

## 회계법인 AI 직무 연결 포인트

회계법인 내부에는 감사 소프트웨어·ERP 연동 스크립트·데이터 파이프라인처럼 오랫동안 유지보수돼 온 사내 시스템이 많다. Junie처럼 실제 디버거로 원인을 확인한 뒤 수정하는 에이전트는, 낯선 레거시 코드에서 "그럴듯해 보이지만 틀린 수정"을 내놓을 위험을 줄여 사내 개발팀의 유지보수 신뢰도를 높일 수 있다.

또한 프로젝트 인식 코드 리뷰 기능은, 감사 데이터 처리 스크립트를 변경할 때 사람이 놓치기 쉬운 부수 효과(다른 모듈에 미치는 영향)를 자동으로 짚어주는 1차 검토 장치로 활용할 수 있다.

면접에서는 "AI 코딩 에이전트를 사내 시스템 유지보수에 도입할 때 무엇을 먼저 검증해야 하는가"라는 질문에, 코드 제안의 그럴듯함이 아니라 실제 실행·디버깅 근거를 갖췄는지를 기준으로 답할 수 있다.

## 핵심 용어·논쟁

- **ACP(Agent Client Protocol)** — 에디터와 AI 코딩 에이전트 사이의 통신을 표준화한 개방형 프로토콜. 벤더 종속 없이 여러 에이전트를 같은 IDE에 연결할 수 있게 한다.
- **Plan Mode** — 실행 전에 에이전트가 작업 계획을 구조화해 제시하는 모드.
- **BYOM(Bring Your Own Model)** — 사용자가 원하는 LLM을 직접 연결해 쓰는 방식.
- **에이전틱 디버깅(Agentic Debugging)** — 코드 추론만이 아니라 실제 디버거를 실행해 근거를 확보하며 수정하는 방식.

ACP처럼 개방형 프로토콜이 확산될수록 "어떤 에이전트를 쓸 것인가"보다 "어떤 IDE·프로토콜 생태계에 속할 것인가"가 더 중요한 선택이 될 수 있다는 시각이 있는 반면, 결국 프로토콜과 무관하게 모델 자체의 성능 차이가 실무 체감을 좌우한다는 반론도 있다.

## 자료 깊이 읽기

### The JetBrains AI Coding Agent moves to general availability — JetBrains 공식 블로그 — 영어, 공식 발표, 초중급
젯브레인즈가 2026년 6월 17일 자사 블로그에 올린 공식 GA 전환 공지다. Junie 전체(에디터 내 에이전트와 독립 CLI 모두)가 베타를 벗어났다고 밝히며, Plan Mode·실제 디버거를 이용한 에이전틱 디버깅·비동기 원격 실행·프로젝트 인식 코드 리뷰·ACP를 통한 IDE-CLI 단일 엔진·BYOM(로컬 런타임 포함)을 GA 단계의 핵심 기능으로 소개한다. 모든 젯브레인즈 IDE와 터미널의 Junie CLI에서 동일하게 쓸 수 있다는 점도 명시한다.

### Agent Client Protocol(ACP) 공식 소개 페이지 — JetBrains 공식 — 영어, 공식 문서, 중급
ACP가 무엇인지, 왜 만들어졌는지를 설명하는 젯브레인즈 공식 페이지다. ACP를 에디터와 AI 코딩 에이전트 사이의 표준 통신 인터페이스로 정의하며, 로컬·원격·사내 자체 개발 에이전트를 벤더 종속 없이 연결할 수 있다는 목적을 밝힌다. 젯브레인즈가 Zed와 공동 개발했고, IntelliJ IDEA·PyCharm·WebStorm 등 전체 IDE 라인업으로 확대 적용 중이라는 배경도 함께 다룬다.

**그 외 참고**
- [Bring your own AI agent to JetBrains IDEs — JetBrains 공식 블로그](https://blog.jetbrains.com/ai/2025/12/bring-your-own-ai-agent-to-jetbrains-ides/) — 영어, 공식 블로그, 중급
- [Coding AI Agent by Jetbrains - Junie — YouTube(Telusko)](https://www.youtube.com/watch?v=ECbmFVahdho) — 영어, 유튜브, 초급
- [Junie Livestream #5: Inner Workings of an AI Coding Agent — YouTube(JetBrains)](https://www.youtube.com/watch?v=z1lVsLPXn2c) — 영어, 유튜브, 중급

유튜브 자료는 이번 환경에서 유튜브 접속 자체가 차단돼 자막을 직접 확인하지 못했다. 따라서 상세 요약 파일을 만들지 않고 제목·링크만 남긴다(검색 결과에 실제로 등장한 URL).

## 자가 점검 질문

1. Junie의 "에이전틱 디버깅"이 단순 코드 추론 기반 수정과 근본적으로 어떻게 다른가?
2. ACP 같은 개방형 에이전트-에디터 프로토콜이 확산되면, 조직의 AI 코딩 도구 선택 기준은 어떻게 바뀔 수 있는가?
3. 사내 레거시 시스템 유지보수에 AI 코딩 에이전트를 투입할 때, 신뢰도를 확인하기 위해 어떤 절차를 먼저 요구해야 하는가?
