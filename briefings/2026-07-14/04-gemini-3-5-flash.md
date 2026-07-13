# 오늘의 AI 개념: Gemini 3.5 Flash 출시

> 작성일: 2026-07-14 · 분류: trend

## 한 줄 정의

구글이 2026년 5월 공개한 신형 경량·고속 AI 모델로, 속도를 크게 높이면서도 코딩·에이전트 작업 성능을 이전 세대보다 끌어올렸다.

## 쉬운 설명

기존 고성능 모델이 짐을 가득 싣고 천천히 움직이는 대형 트럭이라면, Flash는 짐을 나눠 빠르게 여러 번 왕복하는 소형 트럭에 가깝다. 다른 최상위 모델보다 초당 출력 토큰 수 기준으로 4배 빠르면서도, 코딩·에이전트 벤치마크에서는 이전 세대 모델(Gemini 3.1 Pro)을 앞선다.

경량 모델은 보통 "빠르지만 성능이 낮다"는 통념이 있었는데, 이번 모델은 속도와 성능을 동시에 갖췄다는 점에서 그 통념을 깨는 사례로 소개되고 있다. 같은 계열의 고성능 모델(Pro급)과 비교하면 정밀도보다 처리량과 비용 효율을 우선한 설계다.

## 비슷한 것과 비교

| 구분 | 목적 | 속도 | 비용 | 대표 지표 |
|------|------|------|------|----------|
| Gemini 3.5 Flash | 경량·고속 처리 | 타 최상위 모델 대비 4배 | 상대적으로 저렴 | Terminal-Bench 2.1 76.2% |
| Gemini 3.1 Pro(이전 세대) | 고정밀 처리 | 상대적으로 느림 | 상대적으로 고가 | Flash 대비 낮은 에이전트 벤치마크 점수 |

대량의 문서를 빠르게 훑어야 하는 업무는 Flash, 정밀한 판단이 필요한 소수 사례는 Pro급 모델로 나눠 쓰는 것이 합리적인 선택 기준이다.

## 구체 예시·사례

Gemini 3.5 Flash는 에이전트가 터미널 작업을 수행하는 능력을 재는 Terminal-Bench 2.1에서 76.2%, 도구 활용 능력을 재는 MCP Atlas에서 83.6%, 실무 가치 평가 벤치마크인 GDPval-AA에서 1656 Elo를 기록했다. 구글은 "개발자가 며칠 걸리던 일이나 감사인이 몇 주 걸리던 일을 훨씬 짧은 시간에 끝낼 수 있다"고 소개했다.

## 왜 지금 중요한가

Gemini 3.5 Flash는 2026년 5월 19일 Google I/O 2026에서 공개되었으며, Gemini 앱과 구글 검색의 AI 모드, 개발자용 Google Antigravity·Gemini API, 기업용 Gemini Enterprise Agent Platform 등 여러 채널로 순차 제공되고 있다. 발표 시점이 이번 브리핑 작성일 기준 약 2개월 전으로, 신선도 기준(3개월 이내)에 부합한다.

- [Gemini 3.5: frontier intelligence with action](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-5/)
- [Gemini 3.5 Flash is here: Google's smartest speed model promises better coding and agents](https://www.androidauthority.com/google-gemini-3-5-flash-3668559/)

## 회계법인 AI 직무 연결 포인트

계약서나 공시자료처럼 분량이 많은 문서를 신속하게 분류·요약해야 하는 업무에 비용 효율이 높은 경량 모델을 활용할 가능성이 생긴다.

에이전트형 코딩·도구 활용 벤치마크에서의 강세는 사내 감사 자동화 툴을 자체 개발하는 속도를 높이는 데 도움이 될 수 있다.

업무 성격에 따라 여러 모델(예: Claude Sonnet 5, GPT-5.6, Gemini 3.5)을 나눠 쓰는 멀티모델 전략이 회계법인 AI 조직의 표준 운영 방식으로 자리잡아가는 흐름과 맞닿아 있다.

## 핵심 용어·논쟁

- MCP Atlas — 에이전트가 도구를 다루는 능력을 측정하는 벤치마크.
- Terminal-Bench — 에이전트의 터미널 작업 수행 능력을 측정하는 벤치마크.
- GDPval(GDPval-AA) — 실제 업무 가치 창출 능력을 평가하는 벤치마크.
- Elo 점수 — 상대적 성능 순위를 매기는 점수 체계(원래 체스 랭킹 방식에서 유래).

## 자료 깊이 읽기

### Gemini 3.5: frontier intelligence with action (Google 공식 블로그) — 영어, 공식 발표 자료, 중급
(요약 불가 — 본문 확인 실패. 접근이 차단되어 검색 결과로 노출된 개요 수준의 정보만 확인했다.)

### Google I/O 2026: Gemini 3.5 Flash, Spark & Agentic AI — 영어, 블로그 요약, 입문
(요약 불가 — 본문 확인 실패. 검색 결과 제목과 개요만 확인했다.)

**그 외 참고**
- [Gemini 3.5 Flash for Coding and Agents: Setup, Benchmarks, and Honest Best Practices (2026)](https://ofox.ai/blog/gemini-3-5-flash-coding-agents-guide-2026/) — 영어, 블로그, 중급
- [【Google I/O 2026まとめ】Gemini 3.5 Flash・Gemini Omni Flash・Antigravity 2.0まで新AIを全部解説](https://www.youtube.com/watch?v=OmfWgg5MRok) — 일본어, 유튜브 영상, 입문
- [Gemini 3.5 Flash: New Pricing, 4x Speed & Thinking Level Changes](https://webscraft.org/blog/gemini-35-flash-pislya-google-io-2026-nova-model-novi-tsini-i-chomu-defolt-thinking-zminivsya?lang=en) — 영어, 블로그, 입문

## 자가 점검 질문

1. 경량 모델과 고성능 모델을 회계·감사 업무에서 어떤 기준으로 나눠 써야 하는가?
2. MCP Atlas나 Terminal-Bench 같은 벤치마크 점수가 실제 감사 자동화 업무 품질과 어느 정도 상관관계가 있다고 볼 수 있는가?
3. 여러 모델을 병행 사용하는 멀티모델 전략을 도입할 때, 회계법인 입장에서 데이터 보안·거버넌스 측면에서 무엇을 먼저 점검해야 하는가?
