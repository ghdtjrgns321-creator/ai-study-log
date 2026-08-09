# 오늘의 AI 개념: 에이전트 플러그인(Agent Plugins) 오픈 표준

> 작성일: 2026-08-10 · 분류: agentic-coding

## 한 줄 정의

여러 회사의 AI 코딩 도구에서 하나의 확장 기능(플러그인)을 그대로 재사용할 수 있게 만드는 공동 규격이다.

## 쉬운 설명

지금까지 개발자가 AI 에이전트용 확장 기능을 만들면, Cursor용·GitHub Copilot용·Codex용을 각각 따로 포장해야 했다. 같은 기능인데도 도구마다 설정 파일 형식과 폴더 구조가 달랐기 때문이다. Agent Plugins는 이 반복 작업을 없애기 위해 만들어진 공통 패키지 규격이다.

비유하자면 이는 콘센트 규격과 비슷하다. 전자제품 회사마다 플러그 모양이 제각각이면 여행할 때마다 어댑터가 필요하지만, 표준 규격이 있으면 어느 나라 콘센트에도 그대로 꽂을 수 있다. Agent Plugins는 AI 에이전트 확장 기능에 이런 표준 콘센트 모양을 부여한 것이다.

기존에도 Anthropic의 에이전트 스킬(Agent Skills)이나 MCP(Model Context Protocol) 서버 같은 개별 표준은 있었다. Agent Plugins는 이 둘을 없애거나 대체하지 않고, `skills/` 폴더와 `mcp.json`을 하나의 배포 단위(`plugin.json` 매니페스트)로 묶어 여러 클라이언트가 동시에 인식하게 만드는 상위 포장지 역할을 한다.

## 동작 원리

1. 개발자가 플러그인 폴더를 만들고 최상위에 `plugin.json`(이름·버전 등 식별 정보)을 둔다.
2. 그 안에 `skills/` 폴더(재사용 가능한 지시문·리소스)와 `mcp.json`(외부 도구·데이터 연결 정보, stdio·HTTP 방식 지원)을 선택적으로 넣는다.
3. 클라이언트별로 다른 동작이 필요하면 역도메인 이름(예: `com.example.client`)의 하위 폴더에 클라이언트 전용 설정을 추가한다.
4. 호환 클라이언트(ChatGPT, Codex, Cursor, GitHub Copilot, Kiro, VS Code 등)는 이 표준 폴더 구조를 자동으로 인식해 스킬과 MCP 서버를 로드한다.

## 비슷한 것과 비교

| 표준 | 담당 범위 | 강점 | 한계 | 언제 쓰나 |
|------|-----------|------|------|-----------|
| MCP(Model Context Protocol) | 에이전트-외부 도구·데이터 연결 | 도구 호출 프로토콜 자체를 표준화 | 배포 패키징 형식은 다루지 않음 | 외부 API·DB 연동 |
| Agent Skills | 에이전트 지시문·리소스 재사용 | 프롬프트·워크플로 재사용 | 단독으로는 클라이언트 간 이식 규격 없음 | 반복 작업 절차화 |
| Agent Plugins | 위 둘을 하나의 배포 패키지로 통합 | 여러 클라이언트에 동일 패키지 재사용 | 아직 초기 버전(1.0.0), 생태계 미성숙 | 확장 기능을 여러 도구에 동시 배포 |

한 번만 패키징해 여러 에이전트 클라이언트에 그대로 쓰고 싶다면 Agent Plugins, 특정 도구 하나에만 연동하면 되는 단순한 경우라면 MCP·Skills를 개별로 쓰는 편이 가볍다.

## 왜 지금 중요한가

- Vercel이 제안하고 AWS·Cursor(Anysphere)·GitHub·Microsoft·OpenAI가 함께 만든 버전 1.0.0이 2026년 8월 6일 공식 발표됐다. 초기 기술 운영 위원회에도 이들 5개사가 참여한다. [Introducing Agent Plugins](https://vercel.com/blog/introducing-agent-plugins)
- 발표 첫날 소셜 공지 조회수가 110만 회를 넘길 정도로 개발자 커뮤니티의 반응이 컸다. [Agent Plugins: OpenAI, AWS, Cursor, GitHub Standard (2026)](https://explainx.ai/blog/agent-plugins-openai-standard-aws-cursor-github-vscode-2026)
- AWS는 이를 자사 블로그에서 "특정 벤더에 종속되지 않는 이식성"을 핵심 가치로 공식 지지했다. [AWS Supports Agent Plugins](https://aws.amazon.com/blogs/opensource/aws-supports-agent-plugins-an-open-standard-for-portable-agent-extensions/)

## 회계법인 AI 직무 연결 포인트

회계법인이 사내에서 만든 감사 절차용 AI 스킬(예: 계정과목 자동 분류, 전표 이상 탐지 체크리스트)을 Agent Plugins 형식으로 패키징하면, Claude Code·Cursor·GitHub Copilot 등 조직 구성원이 쓰는 여러 도구에서 동일한 절차를 재작성 없이 공유할 수 있다.

벤더 종속을 줄인다는 점도 실무적으로 중요하다. 특정 AI 도구 회사에 감사 워크플로가 묶이면 도구 교체 시 재구축 비용이 크지만, 표준 포맷으로 만들어 두면 도구를 바꿔도 절차 자산은 그대로 이전할 수 있다.

다만 사내 감사 절차를 플러그인으로 배포할 때는 MCP 서버가 접근하는 외부 데이터·시스템 권한 범위를 명확히 통제해야 한다. 표준화가 배포는 쉽게 만들지만, 권한 관리 소홀은 오히려 여러 도구로 위험이 퍼지는 통로가 될 수 있다.

## 핵심 용어·논쟁

- **plugin.json** — 플러그인의 이름·버전 등 식별 정보를 담는 필수 매니페스트 파일.
- **mcp.json** — 플러그인이 연결할 MCP 서버(외부 도구·데이터)를 기술하는 설정 파일.
- **기술 운영 위원회(Technical Steering Committee)** — AWS·Cursor·Microsoft·OpenAI·Vercel의 핵심 유지보수자로 구성된, 표준의 방향을 정하는 조직.
- **역도메인 네임스페이스** — 클라이언트별 확장 설정을 충돌 없이 담기 위해 쓰는 폴더 명명 규칙(예: `com.example.client`).

아직 발표 나흘 남짓 지난 초기 표준이라, 실제로 여러 벤더가 자사 클라이언트에 얼마나 충실히 구현할지, MCP·Skills와의 역할 분담이 장기적으로 어떻게 자리 잡을지는 지켜봐야 하는 단계다.

## 자료 깊이 읽기

### Introducing Agent Plugins (Vercel 공식 블로그) — 영어, 텍스트, 중급
Vercel이 표준을 제안한 배경과 plugin.json·skills·mcp.json으로 구성되는 폴더 구조, 참여 기관(AWS·Cursor·GitHub·Microsoft·OpenAI·Vercel)을 설명한다. 개발자가 확장 기능을 한 번만 만들면 여러 클라이언트에서 재사용할 수 있다는 핵심 가치 제안과, 2026년 8월 6일 발표 사실을 공식적으로 확인할 수 있는 1차 출처다.

### Agent Plugins Specification (agent-plugins.org) — 영어, 텍스트(공식 스펙), 고급
버전 1.0.0 사양 원문. plugin.json 필수 필드, skills 폴더 규격, mcp.json이 지원하는 stdio·Streamable HTTP·HTTP+SSE 연결 방식, 클라이언트별 확장 네임스페이스 규칙을 정의한다. 실제로 플러그인을 만들어보려면 이 문서가 출발점이다.

**그 외 참고**
- [AWS Supports Agent Plugins](https://aws.amazon.com/blogs/opensource/aws-supports-agent-plugins-an-open-standard-for-portable-agent-extensions/) — 영어, 텍스트, 중급
- [Agent Plugins Specification GitHub 저장소](https://github.com/agentplugins/agent-plugins-spec) — 영어, 코드/문서, 고급
- [Agent Plugins package your skills, tools, and more (Google Developers Blog)](https://developers.googleblog.com/agent-plugins-package-your-skills-tools-and-more/) — 영어, 텍스트, 중급

## 자가 점검 질문

1. Agent Plugins가 MCP·Agent Skills를 대체하는 것이 아니라 보완하는 이유는 무엇인가?
2. 회계법인이 사내 감사 절차를 플러그인으로 패키징할 때 가장 먼저 통제해야 할 위험은 무엇인가?
3. 벤더 5개사가 공동으로 표준을 주도하는 구조가 장기적으로 표준의 안정성에 어떤 영향을 줄 수 있는가?
