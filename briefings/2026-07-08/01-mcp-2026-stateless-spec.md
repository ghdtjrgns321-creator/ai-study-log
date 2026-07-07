# 오늘의 AI 개념: MCP 2026 스펙 개편(Model Context Protocol Stateless Core)

> 작성일: 2026-07-08 · 분류: claude-code

## 한 줄 정의

MCP는 AI 모델이 파일, 데이터베이스, 사내 시스템 같은 외부 도구에 접근하는 방식을 하나의 공통 규격으로 통일한 연결 표준이며, 2026년 7월 28일 확정되는 새 스펙은 이 표준을 서버 한 대에 묶이지 않는 구조로 다시 설계한다.

## 쉬운 설명

MCP(모델 컨텍스트 프로토콜)는 Anthropic이 2024년 11월 공개한 개방형 표준이다. AI 모델이 데이터베이스, 사내 시스템, 파일 저장소 같은 외부 도구에 접근하는 방식을 통일해, 도구마다 별도의 연동 코드를 짜야 했던 문제를 줄인다.

MCP는 흔히 "AI용 USB-C 포트"에 비유된다. USB-C 하나로 노트북에 마우스든 모니터든 외장하드든 연결할 수 있듯, MCP를 한 번 구현해두면 AI 모델이 어떤 데이터베이스나 사내 시스템에도 같은 방식으로 접속할 수 있다.

기존 방식으로 AI 도구 N개와 사내 시스템 M개를 서로 연결하려면 N×M개의 개별 연동이 필요했다. MCP는 이 구조를 N+M으로 줄인다. 문서를 검색해 프롬프트에 끼워 넣는 RAG(검색 증강 생성)와 달리, MCP는 AI가 외부 도구를 직접 호출해 실시간으로 조회·실행까지 하게 해주는 연결 표준이라는 점에서 다르다.

2026년 7월 28일 확정 예정인 새 스펙은 이 표준의 내부 동작 방식을 바꾸는 것이지, USB-C 비유 자체를 바꾸는 것은 아니다. 다만 포트 하나에 여러 기기를 물릴 때 특정 포트에만 의존하지 않도록 배선을 다시 깐다는 점에서, 서버 인프라 운영 방식에 실질적인 변화를 가져온다.

## 동작 원리

MCP는 호스트(AI 애플리케이션)-클라이언트-서버의 3단 구조로 동작한다. 기존 스펙에서는 클라이언트가 `initialize` 핸드셰이크를 거쳐 세션 ID를 받고, 이후 요청을 그 세션을 발급한 특정 서버 인스턴스로만 보내야 했다.

2026-07-28 확정 스펙은 이 "상태 유지(stateful)" 구조를 "상태 비저장(stateless) 코어"로 재설계한다. `initialize` 핸드셰이크와 `Mcp-Session-Id` 헤더를 없애고, 프로토콜 정보를 매 요청의 `_meta` 필드에 담아 전달하는 방식으로 바뀐다.

1. 클라이언트가 요청을 보낼 때마다 필요한 프로토콜 정보를 `_meta`에 실어 함께 전송한다.
2. 서버는 어떤 인스턴스든 이 요청을 단독으로 처리할 수 있다. 특정 인스턴스에 세션이 고정될 필요가 없다.
3. 여러 서버 인스턴스를 운영할 때는 일반 라운드로빈 로드밸런서로 트래픽을 분산하면 되고, 별도의 공유 세션 저장소가 필요 없어진다.

같은 개편에서 기존 핵심 기능이던 Tasks(장시간 작업 처리)는 독립적으로 버전 관리되는 Extensions(확장) 체계로 분리됐고, 서버가 제공하는 HTML 화면을 호스트가 샌드박스 iframe에서 렌더링하는 MCP Apps 기능이 새로 추가됐다. 인증 측면에서는 OAuth 2.0·OpenID Connect 표준에 맞춰 인증 응답의 `iss` 파라미터 검증을 의무화하고, `.well-known` 디스커버리 규격을 새로 정의했다.

## 구체 예시·사례

회계법인이 ERP, 감사조서 시스템, 클라우드 스토리지에 흩어진 데이터를 AI 에이전트가 조회하게 하려면, 기존에는 시스템마다 별도 API 연동을 짜야 했다. ERP MCP 서버를 하나 구축해두면, Claude Code 같은 MCP 클라이언트는 표준화된 방식으로 "이번 분기 매출채권 잔액을 조회해줘"라는 요청을 보내고 결과를 감사 조서 작성에 바로 활용할 수 있다.

스펙이 stateless로 바뀌면, 이런 MCP 서버를 여러 대 운영하는 IT팀 입장에서는 특정 서버 인스턴스가 응답을 멈춰도 다른 인스턴스가 대신 요청을 받으면 되므로, 일반적인 로드밸런서 하나만 두면 된다. 이미 인증 계층에서도 변화가 나타나고 있다. 2026년 6월 18일 stable로 승격된 Enterprise-Managed Authorization(EMA) 확장은 사용자가 한 번 로그인하면 조직이 사전 승인한 MCP 서버에 앱별 OAuth 동의 절차 없이 접속하게 해주며, Anthropic·Microsoft·Okta와 Asana·Atlassian·Figma·Linear 등이 이를 지원한다.

## 비슷한 것과 비교

| 구분 | 연결 대상 | 통합 비용 | 실시간 실행 | 대표 사례 |
|------|-----------|-----------|--------------|-----------|
| 개별 REST API 연동 | 시스템마다 1:1 | N×M (도구·시스템 수에 비례) | 가능 | 사내 시스템별 커스텀 연동 |
| RAG | 문서·지식베이스 | 검색 파이프라인 구축 필요 | 조회 위주(실행 불가) | 사규·매뉴얼 검색 |
| MCP | 표준화된 서버 규격 | N+M으로 축소 | 가능(도구 호출·실행) | Claude Code의 파일·DB·API 연동 |

선택 기준은 "AI가 외부 시스템을 실시간으로 조회하고 조작까지 해야 하는가"다. 그렇다면 MCP가, 정적 문서 검색이 목적이라면 RAG가 적합하다.

## 왜 지금 중요한가

MCP 스펙의 릴리스 후보(RC)는 2026년 5월 21일 잠겼고, 최종 스펙은 2026년 7월 28일 확정된다. 공식 블로그는 이번 개편을 "MCP 출시 이후 가장 큰 규모의 프로토콜 수정"이라고 밝혔다.

MCP TypeScript·Python SDK는 2026년 3월 기준 월 9,700만 다운로드를 기록했고, 공개 등록된 MCP 서버도 1만 개를 넘어섰다. 2026년 6월 18일에는 Enterprise-Managed Authorization이 preview에서 stable로 승격돼 기업 단위 접근 통제가 실질적으로 가능해졌다.

- [The 2026-07-28 MCP Specification Release Candidate (Model Context Protocol Blog)](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)
- [Enterprise-Managed Authorization: Zero-touch OAuth for MCP (Model Context Protocol Blog)](https://blog.modelcontextprotocol.io/posts/enterprise-managed-auth/)
- [AI Model Context Protocol Adds Centralised Auth for Enterprise (InfoQ, 2026-07-06)](https://www.infoq.com/news/2026/07/mcp-ema-enterprise-auth/)

## 회계법인 AI 직무 연결 포인트

회계법인은 ERP, 감사조서 관리 시스템, 문서관리시스템(DMS), 클라우드 스토리지 등 이질적인 시스템을 동시에 다룬다. MCP 서버를 시스템별로 구축해두면, AI 에이전트가 매출채권·재고·전표 데이터를 표준화된 방식으로 조회해 감사 절차에 활용할 수 있다.

인증 강화(EMA)는 회계법인처럼 고객 재무 데이터를 다루는 조직에 특히 중요하다. 사용자별로 개별 OAuth 동의를 거치는 대신, 조직의 ID 공급자(IdP)를 통해 접근 가능한 MCP 서버를 중앙에서 통제할 수 있어, 감사 대상 데이터에 누가 어떤 도구로 접근했는지 추적하기 쉬워진다.

stateless 전환은 감사 시즌처럼 여러 팀이 동시에 AI 도구를 몰아 쓰는 성수기에 실질적인 이점이 있다. 서버 인스턴스를 늘려도 특정 세션이 특정 서버에 묶이지 않으므로, 인프라 담당자가 트래픽 급증에 유연하게 대응할 수 있다.

## 핵심 용어·논쟁

- **스테이트리스(Stateless) 코어** — 요청을 처리하는 서버 인스턴스가 고정되지 않고, 어떤 인스턴스든 요청을 받을 수 있는 구조.
- **MCP 서버/클라이언트** — 서버는 외부 도구·데이터를 노출하는 쪽, 클라이언트는 AI 애플리케이션(호스트) 내부에서 서버를 호출하는 쪽.
- **Extensions(확장)** — 공식 스펙과 분리된 저장소에서 독립적으로 버전 관리되는 부가 기능 체계. Tasks(장시간 작업)도 여기로 이동했다.
- **MCP Apps** — 서버가 제공하는 HTML 인터페이스를 호스트가 샌드박스 iframe에서 렌더링하는 기능.
- **EMA(Enterprise-Managed Authorization)** — 조직의 ID 공급자를 통해 MCP 서버 접근을 중앙에서 통제하는 인증 확장.

논쟁 지점: 스펙 개편으로 `initialize` 핸드셰이크와 세션 헤더가 사라지면서, 기존 세션 기반으로 구현된 MCP 서버·클라이언트는 마이그레이션이 필요하다. 보안 매체들은 이 개편이 로드밸런싱을 단순화하는 동시에, 인증·인가 로직을 자체 구현해야 하는 서버 운영자에게는 새로운 검증 부담을 지운다고 지적한다.

## 자료 깊이 읽기

### The 2026-07-28 MCP Specification Release Candidate (Model Context Protocol Blog) — 영어 / 텍스트 / 중급
MCP 공식 블로그가 밝힌 스펙 개편의 배경과 세부 내용이다. Stateless 코어로의 전환이 핵심이며, `initialize` 핸드셰이크와 `Mcp-Session-Id` 헤더를 없애고 프로토콜 정보를 매 요청의 `_meta`에 담는 방식으로 바뀐다. Extensions 프레임워크는 확장 기능을 공식 스펙과 분리된 저장소에서 독립 버전 관리하게 하며, Tasks는 이 체계로 편입됐다. MCP Apps는 서버 제공 HTML을 호스트가 샌드박스 iframe에서 렌더링하게 한다. 인증은 OAuth 2.0·OpenID Connect와의 정렬을 강조해 `iss` 파라미터 검증을 의무화하고 `.well-known` 디스커버리 규격을 새로 정의했다. RC는 2026년 5월 21일 잠겼고, 10주 검증 기간을 거쳐 최종 스펙이 2026년 7월 28일 발표된다.

### AI Model Context Protocol Adds Centralised Auth for Enterprise (InfoQ) — 영어 / 텍스트 / 중급
2026년 6월 18일 Enterprise-Managed Authorization(EMA)이 preview에서 stable로 승격된 소식을 다룬다. 기존에는 사용자가 MCP 서버마다 개별적으로 OAuth 동의를 해야 했지만, EMA는 조직의 ID 공급자를 통해 접근 가능한 서버를 사전 승인해두면 사용자가 한 번 로그인한 뒤 별도 설정 없이 접속하게 해준다. 기술적으로는 Identity Assertion JWT Authorization Grant(ID-JAG)를 발급받아 MCP 서버의 인가 서버와 교환하는 방식을 쓴다. Anthropic, Microsoft, Okta가 이를 채택했고, Asana·Atlassian·Canva·Figma·Granola·Linear·Supabase 등 서버 쪽에서도 지원이 확산되고 있다. 이는 여러 조직이 동시에 MCP 서버를 운영하는 엔터프라이즈 환경에서 접근 통제 부담을 크게 줄이는 변화로 평가된다.

**그 외 참고**
- [07. AI 세상의 표준 프로토콜 MCP(Model Context Protocol) (YouTube)](https://www.youtube.com/watch?v=BloUtXhV038) — 한국어, 유튜브, 중급
- [인공지능 최신기술 이해 - MCP(Model Context Protocol) 동작원리 (YouTube)](https://www.youtube.com/watch?v=kramZYPotLE) — 한국어, 유튜브, 초급
- [Enterprise-Managed Authorization: Zero-touch OAuth for MCP (Model Context Protocol Blog)](https://blog.modelcontextprotocol.io/posts/enterprise-managed-auth/) — 영어, 텍스트, 중급

## 자가 점검 질문

1. MCP가 해결하려는 문제는 무엇이며, REST API 개별 연동이나 RAG와는 어떻게 다른가?
2. 이번 스펙 개편에서 stateless 코어 전환이 왜 인프라 운영 부담을 줄이는가?
3. 회계법인이 여러 사내 시스템에 MCP 서버를 도입할 때, 접근 통제(EMA) 관점에서 가장 먼저 점검해야 할 것은 무엇인가?
