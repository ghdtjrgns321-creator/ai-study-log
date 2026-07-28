# 오늘의 AI 개념: 에이전틱 AI 파운데이션과 MCP·A2A 통합 거버넌스(Agentic AI Foundation, AAIF)

> 작성일: 2026-07-29 · 분류: agentic-coding

## 한 줄 정의

여러 회사가 따로 만든 AI 에이전트 연결 표준들을 하나의 중립 기구가 모아 함께 관리하기 시작한 것을 말한다.

## 쉬운 설명

AI가 외부 도구·데이터와 연결되는 표준으로 Anthropic의 MCP(Model Context Protocol)가 있다. 흔히 "AI용 USB-C"에 비유되는데, 기기마다 다르던 케이블이 하나로 통일된 것처럼 AI 연결 방식을 통일했기 때문이다.

문제는 MCP가 "AI ↔ 도구"만 다룬다는 점이다. "AI 에이전트 ↔ 다른 AI 에이전트"가 대화하며 작업을 나누는 규격은 Google이 만든 A2A(Agent2Agent Protocol)가 따로 맡고 있었다. 2025년 12월 Anthropic은 MCP를 리눅스재단 산하 신설 기구 AAIF에 기부했고, Block(goose)·OpenAI(AGENTS.md)가 공동 설립자로, Google·Microsoft·AWS·Cloudflare·Bloomberg가 지원사로 참여했다. 이미 그전(2025년 6월)에 별도로 리눅스재단에 들어가 있던 A2A도 결과적으로 같은 지붕 아래 놓이면서, 두 표준이 한 재단에서 함께 조율되는 구조가 만들어졌다.

이는 07-08에 다룬 "MCP 2026 스펙 개편"과 결이 다르다. 그날은 프로토콜 자체의 기술적 변화를 다뤘다면, 오늘은 그 프로토콜을 "누가 어떻게 관리하는가"라는 거버넌스 변화를 다룬다.

## 동작 원리

```
2025-06  Google, A2A를 Linux Foundation에 기부
2025-12  Anthropic, MCP를 신설 재단 AAIF에 기부
         ├─ 공동 설립: Anthropic·Block(goose)·OpenAI(AGENTS.md)
         └─ 지원: Google·Microsoft·AWS·Cloudflare·Bloomberg
2026-01  MCP Apps 출시 — MCP 첫 공식 확장(대화형 UI 렌더링)
2026-04  3단계 프로젝트 생애주기(Growth→Impact→Emeritus) 정책 승인
2026-05  회원 190개 조직, A2A v1.0 출시, MCP 월간 다운로드 1억 건 이상
```

거버넌스는 자금·전략을 다루는 Governing Board와 코드·스펙을 다루는 Technical Steering Committee로 나뉜다. 하나의 재단이 여러 벤더의 프로토콜을 동시에 관리하다 보니, MCP·A2A 사이의 상호운용 규격을 맞추는 일이 이 재단의 핵심 과제가 됐다.

## 구체 예시·사례

2026년 1월 26일 출시된 MCP Apps가 좋은 예다. 기존 MCP는 도구가 텍스트로만 응답했지만, 이제는 대시보드·입력폼 같은 대화형 UI를 AI 채팅창 안에 직접 렌더링할 수 있다. Anthropic은 출시 당일 Claude에 이 기능을 적용하며 Amplitude·Asana·Box·Canva·Figma·Slack 등 9개 런칭 파트너를 확보했다. 표준이 한곳에 모이자 새 기능이 한 벤더가 아니라 업계 전체로 동시에 퍼지는 속도가 빨라진 사례다.

## 비슷한 것과 비교

| 구분 | MCP | A2A | AGENTS.md |
|---|---|---|---|
| 원 개발사 | Anthropic | Google | OpenAI |
| 연결 대상 | AI 모델 ↔ 도구·데이터 | 에이전트 ↔ 에이전트 | 프로젝트 ↔ 코딩 에이전트 |
| 한 줄 역할 | AI용 USB-C | 에이전트 간 대화 문법 | 에이전트용 프로젝트 안내서 |

선택 기준: 모델에 새 도구·데이터를 붙일 때는 MCP, 서로 다른 벤더의 에이전트끼리 작업을 나눠 맡길 때는 A2A를 쓴다고 구분하면 된다.

## 왜 지금 중요한가

2026년 5월 18일 자 보도자료에 따르면 AAIF 회원은 190개 조직(신규 골드 4개사 포함)으로 늘었고, 정부기관(NSW 주정부, 미 육군)과 국립연구소·대학까지 회원으로 참여했다.

- [Linux Foundation Announces the Formation of the Agentic AI Foundation (AAIF)](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation)
- [Donating the Model Context Protocol — Anthropic 공식 발표](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation)
- [Agentic AI Foundation Adds 43 New Members (2026-05-18 보도자료)](https://aboutus.godaddy.net/newsroom/news-releases/press-release-details/2026/Agentic-AI-Foundation-Adds-43-New-Members-as-Enterprise-and-Government-Adoption-of-Open-Agent-Standards-Accelerates/default.aspx)

## 회계법인 AI 직무 연결 포인트

회계법인이 여러 벤더의 AI 감사 도구를 조합해 쓸 때, MCP·A2A 같은 개방 표준 준수 여부는 "특정 벤더에 종속되지 않고 나중에 교체할 수 있는가"를 판단하는 조달 기준이 될 수 있다.

여러 에이전트가 A2A로 작업을 주고받을 때 메시지 형식이 표준화돼 있으면 "어떤 에이전트가 어떤 근거로 작업을 넘겼는지"를 로그로 재구성하기 쉬워진다. 이는 07-28에 다룬 AI 에이전트 감사증적 요건과 맞닿아 있다. AI 도구 RFP에 "개방형 표준 준수"를 체크리스트로 요구하는 사례도 늘고 있어 IT 감사 실무자가 알아 둘 조달 심사 포인트다.

## 핵심 용어·논쟁

- **MCP** — AI 모델이 외부 도구·데이터에 연결되는 방식을 표준화한 규격.
- **A2A** — 서로 다른 벤더의 AI 에이전트끼리 통신·협업하는 표준 규격.
- **AAIF** — MCP·A2A·goose·AGENTS.md를 관리하는 리눅스재단 산하 중립 기구.
- **AGENTS.md** — 코딩 에이전트에게 프로젝트별 지침을 전달하는 마크다운 표준.

표준화 기구를 표방하지만 이사회 구성이 소수 빅테크 중심이라, "중립"을 내세워도 실제 규칙 제정이 대형 플랫폼 사업자에게 유리한 방향으로 흘러갈 수 있다는 우려가 업계 일각에서 제기된다.

## 자료 깊이 읽기

### Donating the Model Context Protocol — 영어/공식 발표문/중
Anthropic이 2025년 12월 9일 발표한 공식 자료로, MCP 기부 배경과 AAIF 공동 설립 구조를 설명한다. MCP 사용 통계(공개 서버 1만 개 이상, SDK 월간 다운로드 9,700만 건)를 1차 출처로 확인할 수 있다.

### MCP, 대체 이게 뭐길래 난리야? 진짜 쉽게 설명해드림 (YouTube) — 한국어/설명·데모/하
MCP 입문 영상으로, USB-C 비유로 필요성을 설명하고 클라이언트·서버·리소스·툴·샌드박스 구조를 정리한 뒤 ChatGPT에서 Booking.com·Gmail 커넥터를 실제로 연결해 쓰는 과정을 시연한다. 자막을 직접 확인해 정리했다 — **[상세 요약 보기](videos/aaif-mcp-a2a.md)**.

**그 외 참고**
- [MCP Apps — Bringing UI Capabilities To MCP Clients](https://blog.modelcontextprotocol.io/posts/2026-01-26-mcp-apps/) — 영어, 공식 블로그, 중
- [Tour of Agent Protocols: MCP, A2A, AG-UI, A2UI — JNation 2026](https://www.youtube.com/watch?v=AT5crkuQSgg) — 영어, 컨퍼런스 발표, 중상

## 자가 점검 질문

1. MCP와 A2A는 각각 어떤 연결 문제를 풀기 위한 표준이며, 왜 하나의 재단 아래 함께 관리되기 시작했는가?
2. 회계법인이 여러 벤더의 AI 감사 도구를 조합해 쓸 때, 개방형 표준 준수 여부가 왜 조달 심사 기준이 될 수 있는가?
3. 표준화 기구의 거버넌스가 소수 대형 플랫폼 사업자 중심으로 짜여 있을 때 발생할 수 있는 리스크는 무엇인가?
